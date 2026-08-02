# 🏆✨ The "Optimize Resume As Per JD" ATS Torture Chamber ✨🏆
### *a.k.a. "copy of OptimizeResumeAsPerJD — Enhanced" — the n8n workflow that will juice your resume, lie to your ATS, and spam your Telegram*

---

<p align="center">
  <img src="assets/overview-banner.svg" alt="ATS Torture Chamber — Overview Banner" width="800" />
</p>

<p align="center">
  <em>ATS Score → 💯 · JD Keyword Coverage → 100% · Telegram → Cha-ching</em><br>
  <em>"If at first you don't score 95, loop, loop again." — Every dev ever</em>
</p>

> **WARNING:** This README contains sarcasm. If you are a robot with no sense of
> humour, skip straight to [§5 — Requirements](#5-requirements-or-what-you-actually-need-).
> If you are a human, strap in. 🍿

---

## 📑 Table of Contents

1. [What In The Name Of Hiring Is This?](#1-what-in-the-name-of-hiring-is-this-)
2. [Why Does This Exist? (A Tragic Backstory)](#2-why-does-this-exist-a-tragic-backstory-)
3. [The Big Picture (Architecture, Minus The Buzzwords)](#3-the-big-picture-architecture-minus-the-buzzwords-️)
4. [The ATS Death Loop (How The Magic Happens)](#4-the-ats-death-loop-how-the-magic-happens-)
5. [Requirements (Or What You Actually Need)](#5-requirements-or-what-you-actually-need-)
6. [Installation (Import This Sucker)](#6-installation-import-this-sucker-)
7. [Configuration (Turn The Knobs, Break Things)](#7-configuration-turn-the-knobs-break-things-️)
   - 7.4 [Secrets, Scrubbery & Placeholders](#74-️-secrets-scrubbery--placeholders-read-this-or-get-pwned)
8. [How To Use (Triggering The Beast)](#8-how-to-use-triggering-the-beast-)
9. [Node-By-Node Tour (The Fleshy Bits)](#9-node-by-node-tour-the-fleshy-bits-)
10. [File Naming Conventions (Yes, This Gets Its Own Section)](#10-file-naming-conventions-yes-this-gets-its-own-section-️)
11. [The LaTeX Compile Pipeline (Where PDFs Are Born)](#11-the-latex-compile-pipeline-where-pdfs-are-born-️)
12. [Logs & Debugging (Crying With Evidence)](#12-logs--debugging-crying-with-evidence-️)
13. [Known Issues & Pain Points (Spoiler: There Are Many)](#13-known-issues--pain-points-spoiler-there-are-many-)
14. [Troubleshooting Cheat Sheet (When The Loop Loops Forever)](#14-troubleshooting-cheat-sheet-when-the-loop-loops-forever-)
15. [Working On This Workflow (Live REST Editing 101)](#15-working-on-this-workflow-live-rest-editing-101-️)
16. [API Reference (The Boring But Useful Bits)](#16-api-reference-the-boring-but-useful-bits-)
17. [Execution Log (A Hall Of Shame And Triumph)](#17-execution-log-a-hall-of-shame-and-triumph-️)
18. [Roadmap (Things We Keep Meaning To Do)](#18-roadmap-things-we-keep-meaning-to-do-️)
19. [FAQ (Frequently Agonized Questions)](#19-faq-frequently-agonized-questions-)
20. [License & Disclaimers (Lawyer-Approved Cynicism)](#20-license--disclaimers-lawyer-approved-cynicism-️)
21. [Changelog (The Scar Tissue)](#21-changelog-the-scar-tissue-)
22. [Author](#-author)

---

## 1. What In The Name Of Hiring Is This? 🤔

This is an **n8n workflow** that takes a sad, unoptimized resume 📄 and a job
description 🎯, chews on both with an LLM, and **refuses to shut up until the
resume scores ≥ 95%** against that specific JD. Then — and only then — it
compiles the result into a beautiful PDF 🖨️, generates a cover letter 💌, and
shoves both files into your Telegram chat 📨 along with a smug caption.

In plainer terms: it's a **resume-recycling, keyword-stuffing, loop-obsessed
ATS-bait generator** that treats "good enough" like it's a four-letter word.

### 🎯 What It Does (Feature Matrix)

| Feature | Description | Status |
|---------|-------------|--------|
| 📄 **Resume Extraction** | Extracts structured data from your resume using AI | ✅ |
| 🧠 **JD Intelligence** | Analyzes job description for ATS keywords & priority signals | ✅ |
| ✍️ **Smart Rewriting** | Rewrites resume content — bullets, summary, skills — to match JD naturally | ✅ |
| 🔁 **ATS Death Loop** | Rebuilds & re-scores until the resume hits `>= 95` (max 10 iterations) | ✅ |
| 🖨️ **LaTeX PDF Compilation** | Compiles a clean, professional PDF using pdflatex | ✅ |
| 📬 **Telegram Delivery** | Delivers final PDF + Cover Letter directly to your chat | ✅ |
| 📊 **ATS Scoring** | Scores your resume match % with gap analysis (before **and** after) | ✅ |
| 📝 **Cover Letter Gen** | Generates a tailored HTML cover letter | ✅ |

### 🎬 Live Demo

> Watch the n8n workflow process a resume step-by-step — from form submission
> to Telegram delivery. (Media lives in the `assets/` folder of this repo.)

- 🖱️ **[Interactive Workflow Demo](assets/workflow-demo.html)** — click through
  the simulated execution, node by node.
- 📊 **[Download the Presentation](AI_Resume_Optimizer_Presentation.pptx)** —
  a full slide deck of the project.

### 🎭 The Cast of Characters

| Who | What They Do | Mood |
|-----|--------------|------|
| 🤖 **Resume extractor** | Turns your PDF/DOCX into structured JSON | Judgemental |
| 🤖 **JD extractor** | Turns the job posting into skill wishlists | Hungry |
| ✍️ **Writer (OpenRouter Chat Model2)** | Generates the optimized LaTeX resume | Dramatic |
| 🧪 **ATS Score Agent** | Scores the freshly-baked resume | Nitpicky |
| 🔁 **ATS Loop Guard / ATS Check** | The bouncer that decides if you leave the club | Merciless |
| 💌 **Cover Letter Agent** | Writes the "I'm perfect, hire me" letter | Kiss-assy |
| 🧩 **Build Caption + Cover Letter** | Glues the Telegram caption together | OCD |
| 📡 **Telegram nodes** | The final messengers of your dreams | Pushy |

---

## 2. Why Does This Exist? (A Tragic Backstory) 😢

Somewhere in the universe, a perfectly qualified engineer was rejected by an
Applicant Tracking System (ATS) because their resume said "experienced with
stuff" instead of "Terraform, gRPC, and Kafka." 🔥

The ATS is a robot. Robots are literal. If the keyword is not on the page, the
robot assumes you're unqualified. So this workflow was born to **game the
robot** — ethically-ish — by making sure every keyword the JD wants shows up,
verbatim, in the final resume. 🎯

It's not a magic wand. It's a very persistent rubber stamp that loops until
your score crosses the magical **95/100** line, and it does so by:

1. Extracting the JD's priority keywords.
2. Injecting the missing ones into your Skills section (yes, there's an
   auto-fix in there — see the `Prepare compilation ready` node).
3. Re-scoring. Re-suffering. Repeating. 🔄

### 🧠 How The AI Optimization Works (Three-Stage Pipeline)

Behind all the sarcasm is a surprisingly sound **three-stage intelligence
pipeline**:

| Stage | What Happens | AI Magic |
|-------|--------------|----------|
| **1 — Resume Intelligence** | The resume extractor doesn't just copy-paste text | Consolidates multi-role histories, maps projects to employers by date, reassembles fragmented two-column layouts, standardizes date formats (Sept '21 → September 2021) — with strict anti-hallucination rules |
| **2 — JD Intelligence** | The JD extractor runs a **detect-only** analysis | Identifies high-priority keywords ("Required"/"Must"), classifies the domain, maps responsibility types, and builds a placement strategy telling the next stage exactly which skill goes in which resume section |
| **3 — ATS-Optimized Generation** | The LaTeX generator does its thing | Rewrites experience bullets with strong action verbs, injects JD keywords at the right density, reorders skills by JD priority, and outputs clean, compilable LaTeX |

> 🎯 No hallucination. No invented facts. No "trust me, bro" bullet points.

---

## 3. The Big Picture (Architecture, Minus The Buzzwords) 🏗️

```
   ┌─────────────────────┐        ┌─────────────────────┐
   │  Resume (PDF/DOCX)  │        │  Job Description    │
   │  📄                 │        │  🎯                 │
   └─────────┬───────────┘        └─────────┬───────────┘
             │                              │
             ▼                              ▼
   ┌─────────────────────┐        ┌─────────────────────┐
   │  Extract from File1 │        │   (Form webhook)    │
   │  (PDF-only, lol)    │        │  Resume & JD        │
   └─────────┬───────────┘        │  submitted (Webhook)│
             ▼                    └─────────┬───────────┘
   ┌─────────────────────┐                  │
   │  Resume extractor   │◄─────────────────┘
   │  (LLM → JSON)       │
   └─────────┬───────────┘
             ▼
   ┌─────────────────────┐
   │  JD extractor       │
   │  (LLM → JSON)       │
   └─────────┬───────────┘
             ▼
   ┌──────────────────────────────────────────────────────────┐
   │  ═══════════════  THE ATS DEATH LOOP  ═══════════════   │
   │                                                          │
   │  ┌─────────────┐   ┌──────────────────┐   ┌──────────┐  │
   │  │ ATS Loop    │──▶│ Generated resume │──▶│ Prepare  │  │
   │  │ Guard       │   │ unformatted      │   │ compile  │  │
   │  └─────────────┘   └──────────────────┘   └────┬─────┘  │
   │                                                │        │
   │  ┌─────────────┐   ┌──────────────────┐   ┌────▼─────┐  │
   │  │ ATS Check   │◀──│ ATS Score Agent  │◀──│ Compile  │  │
   │  └──────┬──────┘   └──────────────────┘   │ latex    │  │
   │         │                                 └────┬─────┘  │
   │         ▼                                      │        │
   │  ┌──────────────────┐                          │        │
   │  │ If ATS >= 95 ?   │──No──▶ back to loop 🔁   │        │
   │  └────────┬─────────┘                          │        │
   │           │Yes                                 │        │
   │  ══════════════════════════════════════════════╪═══════ │
   └────────────────────────────────────────────────│───────┘
                      ▼                              │
   ┌─────────────────────┐                          │
   │ ATS Score Agent     │◄─────────────────────────┘
   │ (Before, original)  │  (scores your ORIGINAL resume)
   └─────────┬───────────┘
             ▼
   ┌─────────────────────┐
   │ Cover Letter Agent  │
   └─────────┬───────────┘
             ▼
   ┌─────────────────────┐
   │ Build Caption +     │
   │ Cover Letter        │
   └─────────┬───────────┘
             ▼
   ┌─────────────────────┐        ┌─────────────────────┐
   │ Send resume via     │        │ Send Cover Letter   │
   │ telegram 📨         │        │ via Telegram 💌     │
   └─────────────────────┘        └─────────────────────┘
```

**Total: 23 nodes.** Because 22 would have been too modest.

---

## 4. The ATS Death Loop (How The Magic Happens) 🔁

This is the heart of the beast and the reason your n8n instance may or may not
be spinning hot right now. Here's the contract:

### 📜 Loop Contract

| Parameter | Value | Why |
|-----------|-------|-----|
| Target score | `>= 95` | Because "good enough" is for quitters |
| Max iterations | `MAX_ITERATIONS = 10` | Because we DO have limits (barely) |
| Loop exit | `score >= 95 OR score === null OR forceDone` | A happy ending or a shrug |
| Rebuild mode | Active when `iteration > 1` | Because first drafts are trash |

### 🧠 The "REBUILD MODE" Trick

The writer prompt has two personalities crammed into one:

- **Iteration 1** (fresh build): "YOUR TASK: generate the resume from scratch."
- **Iteration 2+** (rebuild): The prompt swaps in a REBUILD MODE block that
  says (paraphrased): *"You previously generated a resume that scored X. Here
  are the gaps the ATS found. Fix ONLY those gaps. Don't start over. Don't be
  cute."*

The literal prompt structure:

```handlebars
{% if $json.iteration > 1 %}
// REBUILD MODE: The previous version scored {{ score }}.
// Gaps: {{ gaps }}
// Fix ONLY these gaps in the existing LaTeX. Keep the same structure.
{% else %}
// YOUR TASK: [original first-build instructions]
{% endif %}
```

This prevents the LLM from having an identity crisis every loop and throwing
away good work. It doesn't always listen, but we pretend it does. 😌

### 🛑 When The Loop Ends

1. The `ATS Score Agent` scores the newly generated resume against the JD.
2. `ATS Check` runs the termination logic (it's the guard with `MAX_ITERATIONS`).
3. If `score >= 95` → the **If ATS Score >= 95** node sends you down the
   golden path → `ATS Score Agent (Before)` scores your *original* resume so
   you can see how sad it was.
4. If not → back to `ATS Loop Guard`, iteration++, suffer again. 🔁

> 🚨 **Do not edit the loop nodes' connection wiring.** The `If` node's FALSE
> branch feeds back into `ATS Loop Guard` and that's what makes the universe
> not explode. Touch it and you get an infinite loop of despair (or worse, a
> linear pipeline — shudder).

---

## 5. Requirements (Or What You Actually Need) ✅

| Requirement | Version/Detail | Excuse |
|-------------|----------------|--------|
| **n8n** | Local instance (this was built against localhost:5678) | Because cloud bills are scary |
| **n8n API key** | From n8n Settings → API | So scripts can PUT while you sleep |
| **OpenRouter API key** | For the LLM calls | Because your resume deserves "gpt-oss-20b:free" |
| **Telegram Bot token** | For the sendDocument calls | So your chat gets blessed |
| **latex.ytotech.com** | Public LaTeX → PDF compile service | We don't ship TeX locally, we're not animals |
| **Python 3.11+** (optional) | For the helper scripts (fixtures, trigger) | Because PowerShell is a hostage situation |
| **A sense of humour** | Essential | Non-negotiable |

### 📋 The Boring Prerequisites Checklist

If the table above is too sarcastic for you, here is the same information in
responsible-parent form:

| # | Requirement | Details |
|---|-------------|---------|
| 1️⃣ | **n8n installed** (self-hosted) | v2.14 or higher recommended |
| 2️⃣ | **OpenRouter API key** 🆓 | [Get one here](https://openrouter.ai) — the free tier runs this whole thing |
| 3️⃣ | **Telegram Bot** 🤖 | Created via [@BotFather](https://t.me/BotFather) |
| 4️⃣ | **Telegram Chat ID** | Your personal/group chat ID (negative for groups) |
| 5️⃣ | **Internet access** 🌐 | To `latex.ytotech.com` & the AI APIs |
| 6️⃣ | **Optional: Google Gemini / OpenAI keys** | Only if you swap the OpenRouter models for native Gemini/GPT nodes |

---

## 6. Installation (Import This Sucker) 📥

1. Open your n8n instance (`http://localhost:5678`).
2. Click **Workflows** → **Create Workflow** → **⋮ menu** → **Import from File**.
3. Select `optimize-resume-ats-workflow.json` (the exported file living next to
   this README in this very folder. Yes, really.).
4. Fix the credentials if n8n asks (OpenRouter, Telegram, HTTP request).
5. Activate the workflow. 🚀
6. Pray.

> ⚠️ If importing gives you a blank stare, verify your n8n version supports
> **HTTP Request v3** nodes and **Form v2** webhooks. The workflow uses the
> modern spice, not the vintage 2019 flavor.

### 🛠️ The Full Setup Ritual (Step By Step, No Skipping)

#### Step 1 — Import the Workflow 📥
1. Open your n8n instance.
2. Go to **Workflows** → click **Import**.
3. Upload the exported JSON file (`optimize-resume-ats-workflow.json` or the
   repo's `OptimizeResumeAsPerJD — Enhanced.json`).
4. The workflow appears with all 23 nodes pre-configured.

#### Step 2 — Configure OpenRouter Credential 🔑
1. In n8n, go to **Settings** → **Credentials** → **Add Credential**.
2. Search for **OpenRouter** (or the OpenAI-compatible chat model credential).
3. Paste your OpenRouter API key.
4. Assign it to all **OpenRouter Chat Model** nodes (Model1 through Model5 + the
   base model — that's six nodes, in case you lost count).

> 💡 You can use the same credential for all nodes.

#### Step 3 — Configure Telegram 📬
1. Open Telegram → search for **@BotFather** → `/newbot` → copy the **Bot Token**.
2. In n8n: **Credentials** → **Add** → **Telegram** → paste the token → Save.
3. Get your **Chat ID**: add the bot to a group (or DM it), send a message,
   then visit `https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates` and read
   `"chat": {"id": ...}`. Groups give you a negative number like `-1001234567890`.
4. Open both `Send resume via telegram` and `Send Cover Letter via Telegram`,
   set the **Chat ID**, and assign your Telegram credential.

#### Step 4 — Fill The Placeholders (Yes, ALL Of Them) 🕵️
Remember §7.4? The exported JSON ships with `YOUR_*` placeholders so strangers
can't hijack your stuff. Fill in `YOUR_TELEGRAM_CHAT_ID`,
`YOUR_TELEGRAM_CREDENTIAL_ID`, `YOUR_OPENROUTER_CREDENTIAL_ID`, and
`YOUR_FORM_WEBHOOK_ID` (or let n8n regenerate the webhook on activation).

#### Step 5 — Activate & Get Your Form URL ✅
1. Toggle **Inactive → Active** (top-right corner).
2. Click the `Resume & JD submitted` Form Trigger node.
3. Copy the **Production URL** — that's your public form URL. 🎉

### 📦 Deployment (Cloudflare Tunnel — No Docker, No ngrok)

This project was deployed with a **Cloudflare Tunnel** for local hosting — your
PC, Python, and a free tunnel. No cloud subscriptions, no "your URL changed
again" drama. 🚀

| Benefit | Why It Matters |
|---------|---------------|
| 🆓 **Free HTTPS** | No "URL changes" drama |
| 🔁 **Stable & persistent** | Long-running tunnel for continuous bots |
| ⚙️ **Auto-configured** | Python script reads tunnel URL & sets env vars automatically |
| 🧘 **Set & forget** | Less mental overhead than ngrok |

#### 1. Install Cloudflare Tunnel 📥
Download from [developers.cloudflare.com](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/) and verify:
```bash
cloudflared --version
```

#### 2. The Automatic Startup Script 🐍
Create `start_n8n.py` in your project folder:

```python
import subprocess, re, os, time, threading

def start_tunnel():
    proc = subprocess.Popen(
        ["cloudflared", "tunnel", "--url", "http://localhost:5678"],
        stdout=subprocess.PIPE, stderr=subprocess.STDOUT, text=True
    )
    for line in proc.stdout:
        match = re.search(r'https://[a-z0-9-]+\.trycloudflare\.com', line)
        if match:
            url = match.group(0)
            os.environ["WEBHOOK_URL"] = url
            os.environ["N8N_PROTOCOL"] = "https"
            os.environ["N8N_HOST"] = url.replace("https://", "")
            print(f"✅ Tunnel URL: {url}")
            break
    proc.wait()

threading.Thread(target=start_tunnel, daemon=True).start()
time.sleep(5)
os.system("n8n start")
```

#### 3. Run Everything 🚀
```powershell
python start_n8n.py
```
It auto-starts the tunnel, extracts the public HTTPS URL, sets
`WEBHOOK_URL`/`N8N_PROTOCOL`/`N8N_HOST`, and starts n8n. The webhook stays
live indefinitely — no URL changes, no manual restarts.

#### 📋 Post-Deployment Checklist
1. 🔑 Add the **OpenRouter** credential (for all model nodes)
2. 🤖 Add the **Telegram Bot** credential (from @BotFather)
3. 🆔 Set **Chat ID** in both Telegram nodes
4. 🔗 Copy the **Production URL** from the Form Trigger
5. 🚀 **Activate** the workflow

---

## 7. Configuration (Turn The Knobs, Break Things) 🎛️

### 7.1 LLM Temperature (The Creativity Dial)

| Model node | Node it feeds | Temperature | Why |
|------------|---------------|-------------|-----|
| OpenRouter Chat Model (base) | Resume extractor | `0.2` | Facts, not fanfiction |
| OpenRouter Chat Model1 | JD extractor | `0.2` | Let's not imagine keywords |
| **OpenRouter Chat Model2** | **Writer** | `0.5` | Slightly dramatic, keeps structure |
| OpenRouter Chat Model3 | ATS Score Agent | `0.2` | Scoring should be sober |
| OpenRouter Chat Model4 | Cover Letter Agent | `0.6` | Sappy letters need a spark |
| OpenRouter Chat Model5 | ATS Score Agent (Before) | `0.2` | Also sober |

Temperature is set via `parameters.options.temperature` on each model node.

### 7.2 Telegram

- **Chat ID:** `YOUR_TELEGRAM_CHAT_ID` (the real one is scrubbed from the
  exported JSON — see §7.4 for the full placeholder rundown).
- **Resume node:** `operation: sendDocument`, `binaryPropertyName: pdfData`.
- **Cover letter node:** `operation: sendDocument`, `binaryPropertyName: coverLetterFile`.

### 7.3 LaTeX Compiler

`Compile latex code` POSTs to:

```
https://latex.ytotech.com/builds/sync
```

With a body like:

```json
{
  "compiler": "pdflatex",
  "resources": [{ "main": true, "content": "\\documentclass... \\end{document}" }]
}
```

- **201** → PDF bytes. 🎉
- **400** → your LLM produced invalid LaTeX. Again. 🙃
- **Retry**: `retryOnFail: true`, `waitBetweenTries: 5000`.

### 7.5 🤖 Supported AI Models (The Pedigree)

This workflow ships wired to **OpenRouter** (`openai/gpt-oss-20b:free`) because
the free tier is a glorious cheat code. But the nodes are model-agnostic — swap
in whatever flavour you fancy. For reference, the original template supported
these families:

#### 🟢 Google Gemini Family

| Model ID | Speed | Quality | Best For |
|----------|-------|---------|----------|
| `models/gemini-2.0-flash-lite-001` | ⚡⚡⚡ | ✅ | Resume/JD Parsing (fast) |
| `models/gemini-2.5-flash-image` | ⚡⚡⚡ | ✅✅ | Parsing + Reasoning |
| `models/gemini-3.1-flash-image-preview` | ⚡⚡ | ✅✅✅ | LaTeX Generation |
| `models/gemini-3-pro-image-preview` | ⚡ | ✅✅✅✅ | ATS Scoring, Cover Letter |

#### 🔵 OpenAI Family

| Model ID | Speed | Quality | Best For |
|----------|-------|---------|----------|
| `gpt-5-mini` | ⚡⚡⚡ | ✅ | Fast parsing tasks |
| `gpt-5.4-image-2` | ⚡⚡ | ✅✅✅ | Advanced gen + reasoning |

#### 🟣 OpenRouter (current default)

| Model ID | Notes |
|----------|-------|
| `openai/gpt-oss-20b:free` | Free, shockingly competent, zero guilt |

> 💡 Models are also listed in `config.json` for reference. To switch models,
> just change the `model` parameter on each OpenRouter Chat Model node and
> re-import.

### 7.6 🧱 The ATS Scoring Engine (The Nitpicky Math)

The ATS Score Agent uses a **4-factor weighted scoring model** — yes, there is
actual arithmetic behind the sarcasm:

```
ATS Score = (Keyword Coverage × 0.40) + (Skills Alignment × 0.30)
          + (Experience Relevance × 0.20) + (Role Title Match × 0.10)
```

#### 📈 Score Interpretation

| Score Range | Recommendation | Visual |
|-------------|---------------|--------|
| 80–100 | 🚀 Strong Match | 🟩🟩🟩🟩🟩🟩🟩🟩🟩🟩 |
| 60–79 | ✅ Good Match | 🟩🟩🟩🟩🟩🟩🟩🟩⬜⬜ |
| 40–59 | ⚠️ Moderate Match | 🟩🟩🟩🟩🟩⬜⬜⬜⬜⬜ |
| 0–39 | 🔴 Weak Match | 🟩🟩🟩🟩⬜⬜⬜⬜⬜⬜ |

The loop refuses to ship anything below **95** — so if you see a "Good Match"
leave the building, it means the writer was on iteration 10 and gave up. 😬

### 7.7 💌 The Cover Letter Generator (Sappy But Effective)

The Cover Letter Agent writes **5-paragraph HTML cover letters** designed for
email delivery:

| Paragraph | Content | Purpose |
|-----------|---------|---------|
| 1️⃣ | Strong hook with company/role reference | Grab attention |
| 2️⃣ | Why this role & company specifically | Show research |
| 3️⃣ | 2–3 strongest matching achievements (quantified) | Prove capability |
| 4️⃣ | Address biggest skill gap as a learning narrative | Show growth mindset |
| 5️⃣ | Confident, action-oriented closing | Drive response |

> 🎨 Output is clean HTML with inline CSS — works in Gmail, Outlook, etc. Sent
> to Telegram as a `.html` attachment because PDFs are for the resume only.

### 7.4 🕵️ Secrets, Scrubbery & Placeholders (Read This Or Get Pwned)

The exported `optimize-resume-ats-workflow.json` is **deliberately scrubbed**.
Any value that could let a stranger hijack your bot, drain your API credits, or
spam your chat is replaced with an angry-looking `YOUR_...` placeholder. That's
not a bug. That's self-preservation. 🛡️

The real values live only in your live n8n instance (and in whatever vault your
paranoia prefers). When you import the JSON, **you must fill the placeholders
back in** or the workflow will refuse to run / silently no-op.

Here is the complete inventory. Learn it. Live it. Replace it. 📋

| Placeholder | What It Is | Where It Lives (in the JSON) | What To Put There |
|-------------|------------|------------------------------|-------------------|
| `YOUR_FORM_WEBHOOK_ID` | The trigger ID that makes your web form reachable at `http://localhost:5678/form/<id>` | Node `Resume & JD submitted` → top-level `webhookId` | The `webhookId` shown on the node in the n8n editor (the UUID after `/form/`). If missing, n8n regenerates one on activation. |
| `YOUR_TELEGRAM_CHAT_ID` | The chat/group/channel your bot posts files into | Nodes `Send resume via telegram` and `Send Cover Letter via Telegram` → `parameters.chatId` | Your Telegram chat ID, e.g. `-1001234567890` for a group. Get it from a bot like `@userinfobot` or by watching the update stream. |
| `YOUR_TELEGRAM_NODE_WEBHOOK_ID` | Internal webhook ID on the Telegram nodes (leftover from the original template) | Nodes `Send resume via telegram` and `Send Cover Letter via Telegram` → top-level `webhookId` | Whatever n8n assigns on import. This field is **not used** for `sendDocument`, so a random UUID is fine. |
| `YOUR_TELEGRAM_CREDENTIAL_ID` | The credential ID that points to your Telegram bot token | Telegram nodes → top-level `credentials.telegramApi.id` | The credential UUID shown in **n8n → Credentials**. Re-associate the credential in the node instead of hand-editing if you can. |
| `YOUR_OPENROUTER_CREDENTIAL_ID` | The credential ID that points to your OpenRouter API key (all 6 model nodes) | OpenRouter model nodes → top-level `credentials.openRouterApi.id` | The credential UUID shown in **n8n → Credentials** (OpenRouter). Re-associate via the editor to be safe. |

> 🔐 **Why only IDs and not the keys themselves?** n8n never stores API keys in
> the workflow JSON — it stores a *credential ID* that references the key in
> n8n's credential vault. So scrubbing the IDs (plus webhook IDs and chat ID) is
> sufficient to make the export shareable. The keys themselves were never in the
> file to begin with. Lucky you.

> 🚨 **Sensitive things that are NOT in the JSON but ARE in the README lore:**
> - The n8n API key (`X-N8N-API-KEY`) — never committed; use `YOUR_N8N_API_KEY`.
> - The OpenRouter API key — never committed; lives in the credential.
> - The Telegram bot token — never committed; lives in the credential.

**The golden rule:** if it looks like a real UUID, a real chat ID, or a real
webhook ID when you open the exported file, **stop and scrub it before sharing.**
When in doubt, n8n's own **Workflow → Export → Download** flow is the
blessed path — it strips these automatically. We scrubbed by hand here because
we're control freaks. 🎛️

---

## 8. How To Use (Triggering The Beast) 🚀

### 8.1 The Fancy Way: Web Form

The workflow exposes an n8n **Form v2** webhook:

```
http://localhost:5678/form/YOUR_FORM_WEBHOOK_ID
```

The form has **two** fields. Do NOT trust the labels. The REAL multipart field
names (verified by peeking at the generated HTML, because labels lie) are:

| Multipart field | Content | Description |
|-----------------|---------|-------------|
| `field-0` | File upload | The resume (`.pdf`… or `.docx` if you enjoy pain — see Known Issues) |
| `field-1` | Textarea | The job description |

> 🔑 The `YOUR_FORM_WEBHOOK_ID` placeholder replaces the real webhook trigger
> ID in the exported JSON — see §7.4 for the full placeholder rundown.

### 8.2 The Scripted Way: `trigger-form.ps1` 🐚

There's a PowerShell trigger script that submits the form programmatically via
.NET `HttpClient` multipart:

```powershell
.\trigger-form.ps1 -Resume "sample-resume.pdf" -Jd "sample-jd.txt"
```

**CRITICAL GOTCHA discovered by blood, sweat, and tears:** the JD text MUST be
sent as `ByteArrayContent` **WITHOUT** a `Content-Type` header or filename. If
you send it as `StringContent` (text/plain), n8n treats it as an *uploaded
file* and the JD lands in the binary section while the JSON value stays
`null` — which makes the JD extractor feed on air and the whole thing scores
garbage. You don't want that. Trust us.

### 8.3 Sample Fixtures

- `sample-resume.pdf` — generated with reportlab so you don't have to.
- `sample-resume.docx` — the masochist's alternative.
- `sample-jd.txt` — a "Senior Backend Engineer (Python)" JD with the
  nice-to-haves Terraform, gRPC, and Kafka (so the loop has something to chase).

---

## 9. Node-By-Node Tour (The Fleshy Bits) 🔬

### 9.1 Resume & JD submitted (Form Trigger) 📥
The webhook. Everything fun starts here. Captures `field-0` (resume) and
`field-1` (JD). Output JSON keys: `Resume` (file descriptor),
`Job Description 🎯` (text), `submittedAt`, `formMode`. Binary keys:
`Resume`, `Job_Description___`.

### 9.2 Extract from File1 🗂️
Extracts text from the uploaded file. **PDF ONLY.** Yes, the form happily
accepts `.docx`. No, the extractor does not care. It will gleefully error with
`Invalid PDF structure` if you upload a Word doc. This mismatch is a feature
now. 🔪

### 9.3 Resume extractor (LLM) 🤖
Takes the raw extracted text and produces a strict JSON with the candidate's
name, contact info, skills, work history (one entry per sequential role), and
projects nested under the right job. Heavily prompted to ignore placeholder
names like "Nitin Singh" (we're not bitter, we're thorough).

Key output field: `full_name` — used later for the filename. 🏷️

### 9.4 JD extractor (LLM) 🤖
Parses the job description into:
- `priority_keywords.high` (the "if you don't have this, don't apply" list)
- `must_have_skills`
- `skills.technical_skills`
- `domain`

These feed the keyword-coverage auto-fix AND the writer's REBUILD MODE.

### 9.5 ATS Loop Guard 🔒
The loop's turnstile. Carries `iteration`, `score`, `gaps`, and the resume+JD
payload. Checks `MAX_ITERATIONS` and the termination condition
(`done = score >= 95 || score === null || forceDone`). If done → outputs to
`Generated resume unformatted`… wait, no. If NOT done → writer. If done → the
payload flows to the finish line via a different path. (This is the node you
point the FALSE branch of the `If` back at.)

### 9.6 Generated resume unformatted (Writer LLM) ✍️
The star. Produces LaTeX. Uses the REBUILD MODE prompt on iterations > 1.
Its output is a raw LaTeX blob that will 100% have markdown fences and stray
preamble until `Prepare` fixes it.

### 9.7 Prepare compilation ready 🧹
A Code node that does the heavy lifting:
1. Strips markdown fences (` ```latex `).
2. Cuts everything before `\documentclass`.
3. Cuts everything after `\end{document}`.
4. **ATS keyword auto-fix:** parses the JD extractor output, collects all
   keywords, finds which are missing from the LaTeX, and injects a
   `\item \textbf{JD-Matched Keywords:} <comma-separated escaped keywords>`
   into the Skills section. Then recomputes `keywordCoverage`.
5. Builds `requestBody` for the compile step.
6. Computes `filename` = **candidate name only** (sanitized, spaces → `_`).

Output JSON: `requestBody`, `filename`, `candidateName`, `latexPreview`,
`keywordCoverage`, `missingKeywords`.

### 9.8 Compile latex code ☁️
HTTP Request (v3) to latex.ytotech.com. No local TeX. We outsource the pain.

### 9.9 Compile & convert to pdf file 🧩
Code node that carries the binary `pdfData` forward alongside `filename`,
`candidateName`, and `keywordCoverage`.

### 9.10 ATS Score Agent (LLM) 🧪
Scores the generated resume against the JD. Returns JSON like:

```json
{
  "score": 97,
  "recommendation": "Strong Match",
  "gaps": ["Add Terraform", "Mention gRPC", "Spell Kafka correctly"],
  "top_matching_keywords": ["Python", "AWS", "CI/CD"]
}
```

### 9.11 ATS Check 🔎
Code node. The referee. Computes `done` using the loop contract. Feeds the
`If ATS Score >= 95` node.

### 9.12 If ATS Score >= 95 ⚖️
- **TRUE** → `ATS Score Agent (Before)` (golden path).
- **FALSE** → back to `ATS Loop Guard` (the highway to iteration N+1).

### 9.13 ATS Score Agent (Before) 🤖
Scores the ORIGINAL uploaded resume so your Telegram caption can display the
humbling before/after comparison.

### 9.14 Cover Letter Agent (LLM) 💌
Writes an HTML cover letter. Output wrapped in markdown fences (cleaned in
Build Caption). Self-soothing flattery machine.

### 9.15 Build Caption + Cover Letter 🧩
The Swiss Army code node:
- Parses both ATS JSON scores (before + after).
- Renders the emoji score bar (`scoreBar`).
- Builds the caption with `📄 File: ${resumeFilename}`.
- Cleans the cover letter HTML (strips fences, finds the `<html>` tag).
- Converts HTML → base64 binary for Telegram.
- Computes `resumeFilename` and `coverLetterFilename` from the name-only base.

Output JSON: `caption`, `filename`, `resumeFilename`, `coverLetterFilename`,
`candidateName`, `atsScore`, `beforeScore`, `atsRecommendation`,
`keywordCoverage`, `coverLetterHtml`, `htmlBase64`.

Output binary: `pdfData` (the compiled resume PDF), `coverLetterFile`
(HTML content, `fileName = coverLetterFilename`).

### 9.16 Send resume via telegram 📨
`sendDocument` with `binaryPropertyName: pdfData`, `fileName` =
`={{ $json.filename }}_resume.pdf`.

### 9.17 Send Cover Letter via Telegram 💌
`sendDocument` with `binaryPropertyName: coverLetterFile`, `fileName` =
`={{ $json.filename }}_coverletter.html`.

---

## 10. File Naming Conventions (Yes, This Gets Its Own Section) 🏷️

We fought, we bled, and we ended up with this majestic scheme:

| Artifact | Naming Rule | Example |
|----------|-------------|---------|
| Base name | `{{ $json.filename }}` = **candidate name only**, sanitized (`[^a-zA-Z0-9\s]` stripped, spaces → `_`) | `Alex_Morgan` |
| Resume PDF | `<name>_resume.pdf` | `Alex_Morgan_resume.pdf` |
| Cover letter | `<name>_coverletter.html` | `Alex_Morgan_coverletter.html` |

**Why lowercase suffixes?** Because uppercase is for people who don't debug
their own n8n at 2 AM. Also, the user explicitly asked. 📏

**Where the name comes from:** `Prepare compilation ready` pulls `full_name`
from the `Resume extractor` output via regex:
`/"full_name"\s*:\s*"([^"]+)"/`.

> 📌 **Important:** `filename` itself contains NO extension. The suffixes are
> appended at the Telegram layer. Do not "helpfully" add `_Resume.pdf` back to
> `filename` in `Prepare` — you'll break every downstream node that does
> `$json.filename + "_resume.pdf"` and get `Alex_Morgan_Resume.pdf_resume.pdf`,
> which is the filenaming equivalent of a wardrobe malfunction.

---

## 11. The LaTeX Compile Pipeline (Where PDFs Are Born) 🖨️

```
Writer LLM ──▶ raw LaTeX blob (with fences, junk, hopes)
     │
     ▼
Prepare compilation ready ──▶ cleans → injects keywords → requestBody
     │
     ▼
Compile latex code ──▶ POST latex.ytotech.com/builds/sync
     │
     ├── 201 ──▶ pdfData binary ✅
     │
     └── 400 ──▶ invalid LaTeX from the LLM 😭
```

**Why 400s happen:** The writer is an LLM. LLMs occasionally output
`\href{mailto:}{$|$` or forget a closing `}`. It's not a service outage — the
service is fine (a tiny `"Hello"` doc compiles to 201 in milliseconds). It's
your writer having a bad day. Mitigations: retry, lower temperature, or pray.

**Timeout myth debunked:** n8n's HTTP Request v3 default timeout is actually
**300s** (`requestOptions.timeout = 300_000`), not 60. So a "timeout" error on
a 73-second compile is a red herring — check for a 400 first.

---

## 12. Logs & Debugging (Crying With Evidence) 🕵️

### 12.1 n8n UI
- **Executions** tab → find your execution → inspect each node's input/output.
- Look at `json.output` of the LLM agent nodes (that's where score, gaps,
  keyword lists, and extracted names live).

### 12.2 The raw event log
n8n keeps an event log at:

```
C:\Users\Nitin Kumar\.n8n\n8nEventLog.log
```

Every node start/finish per `executionId` is timestamped there. Grep it when
the UI lies.

### 12.3 API-based inspection
```powershell
$key = "<YOUR_API_KEY>"
Invoke-RestMethod -Uri "http://localhost:5678/api/v1/executions?limit=5" `
  -Headers @{ 'X-N8N-API-KEY' = $key }
```

### 12.4 The compiled-body forensic technique
Save the exact `requestBody` from a failed compile and replay it against
latex.ytotech.com with `curl`. Compare against a known-good body. This is how
we proved the compile failures were bad LaTeX, not a dead service. 🧪

---

## 13. Known Issues & Pain Points (Spoiler: There Are Many) 🩹

| # | Issue | Symptom | Workaround |
|---|-------|---------|------------|
| 1 | Form accepts `.docx` but extractor is PDF-only | `Invalid PDF structure` | Use PDFs. Accept your fate. |
| 2 | `StringContent` JD sends JD as a file | JD JSON value = `null`, scoring is garbage | Send JD as `ByteArrayContent` w/o Content-Type/filename |
| 3 | LLM produces invalid LaTeX | 400 from latex.ytotech.com | Retry / lower temperature / check requestBody |
| 4 | Form labels ≠ multipart names | Wrong field names in trigger script | Use `field-0` / `field-1` |
| 5 | PowerShell BOM breaks PUT bodies | `Failed to parse request body` | Write body without BOM + `curl.exe --data-binary` |
| 6 | Cover letter is HTML but user wanted `.pdf` | Philosophical crisis | Resolved: it stays `.html`. The user is the boss. |
| 7 | `filename` containing extension breaks suffixes | `name_resume.pdf_resume.pdf` | `filename` = name only, period |
| 8 | "The connection timed out" at compile | Panic | It's a 400 in a trench coat. Check requestBody. |
| 9 | Emojis in shell output break consoles | `UnicodeEncodeError` | Run python with `-X utf8` and reconfiguring stdout |
| 10 | LLM sometimes ignores REBUILD MODE | Score doesn't improve across loops | Wait for iteration 3. Or 4. Or 10. |

---

## 14. Troubleshooting Cheat Sheet (When The Loop Loops Forever) 🆘

**Q: The workflow never stops. My fans are screaming.**
A: Check `MAX_ITERATIONS` in `ATS Loop Guard` AND `ATS Check`. Verify the `If`
FALSE branch still feeds `ATS Loop Guard`. If `score` keeps coming back as
`null` (JD parsing failed), the loop bails out with `done = true` — but if the
JD was fine and the LLM just won't cross 95, it's the model, not the wiring.

**Q: ATS score is high but the Telegram files are wrong.**
A: Check `Prepare` output `filename`. If it contains an extension, see
§10. Then check `Build Caption` output `resumeFilename`/`coverLetterFilename`.

**Q: The caption says "File: undefined".**
A: `filename` was `undefined` at caption build time. Make sure `Prepare`
actually emitted `filename` and that `Compile & convert` carried it.

**Q: PDF comes back 400.**
A: Grab `requestBody` from `Prepare`, replay it:
```
curl.exe -s -X POST https://latex.ytotech.com/builds/sync -H "Content-Type: application/json" --data-binary "@requestBody.json"
```
If 400 → bad LaTeX. If 201 → your node config is haunted.

**Q: The JD keyword coverage is 0%.**
A: `JD extractor` output JSON structure doesn't match the parse logic
(`priority_keywords.high`, `must_have_skills`, `skills.technical_skills`).
Inspect the raw extractor output. The LLM renamed a key. They do that.

**Q: I changed a node via the UI and now the API body won't PUT.**
A: `settings` must contain ONLY `executionOrder` on PUT. The UI adds
`binaryMode`, `availableInMCP`, etc., and the API will scream
`request/body/settings must NOT have additional properties`. Strip them.

### 🩺 The Classic Ailments Table (From The Original Template)

The OG README knew a few tricks we kept in the medicine cabinet:

| Error | Likely Cause | Fix |
|-------|-------------|-----|
| `Missing \begin{document}` | LLM wrapped output in markdown fences | ✅ Auto-fixed by `Prepare compilation ready` node |
| `MISSING_COMPILATION_SPECIFICATION` | Double `==` in HTTP body expression | Use single `=`: `={{ $json.requestBody }}` |
| `XeTeXglyph` error | `fontawesome5` package used | Remove `\usepackage{fontawesome5}` from LaTeX skeleton |
| Empty PDF / blank resume | Scanned image PDF | Convert to text-based PDF first, or use DOCX format |
| Telegram bot not sending | Bot not added to group | Add bot to group and make it admin |
| AI API errors | Rate limit on free tier | Add a **Wait** node (5s) between AI agents |

---

## 15. Working On This Workflow (Live REST Editing 101) 🛠️

Because editing a 23-node loop through the UI while it's mid-execution is a
great way to lose your lunch, we edit via the **n8n REST API**. The golden
rules:

### 15.1 The API Contract
- **Base:** `http://localhost:5678/api/v1`
- **Auth header:** `X-N8N-API-KEY: <your-key>`
- **GET:** `GET /workflows/<id>` — fetch the live workflow.
- **PUT:** `PUT /workflows/<id>` — save changes. Body = `{ name, nodes,
  connections, settings }`.

### 15.2 The PUT Body Trap (learned the hard way)
```json
{
  "name": "copy of OptimizeResumeAsPerJD — Enhanced",
  "nodes": [ ... ],
  "connections": { ... },
  "settings": { "executionOrder": "v1" }
}
```
- Only `name`, `nodes`, `connections`, `settings`.
- `settings` → ONLY `executionOrder`. Not `binaryMode`. Not
  `availableInMCP`. **NOTHING ELSE.** 🔨
- PATCH is rejected (405) on this n8n. PUT or GTFO.

### 15.3 The BOM Trap (also learned the hard way)
- Write the body as **UTF-8 without BOM**.
- Send with `curl.exe --data-binary "@body.json"`.
- `Invoke-RestMethod -InFile` will betray you with a BOM and
  `body-parser` will reject the whole thing.

### 15.4 Editing Flow
1. `GET /workflows/<id>` → save snapshot.
2. Modify the node(s) in a script (Python is kinder to unicode/emojis than
   PowerShell string munging — the captions are full of 📄🟩⬜🎯).
3. Build the PUT body, write no-BOM, `curl.exe --data-binary`.
4. Check `versionId` increments in the response.
5. Re-trigger and watch the Executions tab like a hawk. 🦅

---

## 16. API Reference (The Boring But Useful Bits) 📚

### Endpoints used

| Method | URL | Purpose |
|--------|-----|---------|
| GET | `/api/v1/workflows/<id>` | Fetch workflow |
| PUT | `/api/v1/workflows/<id>` | Update workflow |
| POST | `/api/v1/workflows/<id>/activate` | Activate |
| POST | `/api/v1/workflows/<id>/deactivate` | Deactivate |
| GET | `/api/v1/executions?limit=N` | List executions |
| GET | `/api/v1/executions/<id>` | Execution detail |

### External services

| Service | Endpoint | Used for |
|---------|----------|----------|
| OpenRouter | (via n8n OpenAI-compatible credential) | All LLM calls |
| LaTeX | `https://latex.ytotech.com/builds/sync` | PDF compilation |
| Telegram | Bot API (via n8n node) | File delivery |
| n8n Form | `http://localhost:5678/form/YOUR_FORM_WEBHOOK_ID` | Manual trigger |

### Data shapes

**Resume extractor** → JSON containing `full_name`, contact, experience
(one entry per role), skills, projects.

**JD extractor** → `{ priority_keywords: { high: [] }, must_have_skills: [],
skills: { technical_skills: [] }, domain: ... }`

**ATS Score Agent** → `{ score, recommendation, gaps: [], top_matching_keywords:
[] }`

**Prepare** → `{ requestBody, filename, candidateName, latexPreview,
keywordCoverage, missingKeywords }`

**Build Caption** → `{ caption, filename, resumeFilename, coverLetterFilename,
candidateName, atsScore, beforeScore, atsRecommendation, keywordCoverage,
coverLetterHtml, htmlBase64 }`

---

## 17. Execution Log (A Hall Of Shame And Triumph) 🏛️

| # | Status | The Drama |
|---|--------|-----------|
| 347 | ✅ success | Warm-up run |
| 348 | ✅ success | Another warm-up. Weird vibes. |
| 349 | ❌ error | `Invalid PDF structure` — someone sent a `.docx` to a PDF-only extractor. Rookie mistake. |
| 350 | ✅ success | JD was `null` (wrong field names). Still scored 97. The LLM hallucinated its way to victory. |
| 351 | ✅ success | JD still `null` (StringContent → treated as file). ATS 98. Gaps: Terraform, gRPC, Kafka. |
| 352 | ❌ error | "The connection timed out" at compile. It was actually a 400 in a trench coat. |
| 353 | ❌ error | **JD fix verified!** JD parsed as String (1359 chars). Then compile → 400. The writer wrote `\href{mailto:}{$|$`. We keep receipts. |
| 354 | ✅ success | Full clean run. Compile worked. Both Telegram sends fired. The loop earned its keep. |

---

## 18. Roadmap (Things We Keep Meaning To Do) 🗺️

- [ ] Make `Extract from File1` accept `.docx` so the form stops lying.
- [ ] Convert the cover letter to a real PDF so the `.pdf` filename makes sense.
- [ ] Add a resume-vs-resume A/B score breakdown in the Telegram caption.
- [ ] Persist `MAX_ITERATIONS` as a workflow-level setting instead of a magic constant.
- [ ] Auto-retry failed LaTeX compiles with a "please fix your LaTeX" nudge to the writer.
- [ ] Sanitize the caption so emojis don't break Python consoles (we just work around it).
- [ ] A dashboard. Everyone wants a dashboard. (No one will maintain it.)

### 💡 Enhancement Ideas (Borrowed From The OG, Still Unbuilt)

The original template came with a delightful wishlist. We kept it because we,
too, like to dream:

- 📧 **Email Delivery (Gmail):** Add a **Gmail node** after `Compile & convert
  to pdf file` to send the PDF + Cover Letter as an email attachment. Great for
  sharing directly with recruiters.
- ⚡ **Parallel AI Processing:** Wire `Resume extractor` and `JD extractor`
  straight from `Extract from File` to run in parallel — cuts processing time
  by ~40%!
- 📨 **Instant Acknowledgement:** Add a Telegram/Gmail node right after the
  Form Trigger: *"✅ We've received your resume. Your optimized version will
  arrive in ~90 seconds."*
- 🔔 **Error Alerts via Telegram:** An **Error Trigger** workflow that DM's you
  the full error details when any node fails.
- 📊 **Google Sheets Logging:** Log candidate name, JD domain, ATS score,
  timestamp — for usage tracking.
- 🌐 **Multi-language Support:** Detect resume language and generate the
  optimized resume in the candidate's preferred language.
- 🧪 **A/B Testing Mode:** Generate 2 resume versions with different keyword
  strategies and let you pick the better ATS score.
- 🏢 **Company Research Agent:** Add a web search node that researches the
  company before generating — even more tailored content.
- 💾 **Version History:** Store all generated resumes with version tracking —
  compare & revert anytime.

---

## 19. FAQ (Frequently Agonized Questions) ❓

**Q: Does this guarantee I get the job?**
A: Absolutely not. It guarantees the ATS robot sees the keywords. The human
recruiter may still hate you. That's their problem. 🤷

**Q: Is gaming the ATS ethical?**
A: That's between you and your conscience. We're a workflow, not a therapist.

**Q: Why is the temperature 0.5 on the writer?**
A: High enough to be creative, low enough to mostly produce valid LaTeX.
"Mostly" is doing a lot of heavy lifting here. 😅

**Q: Why does the form say `.docx` is OK?**
A: Great question. Ask the original author. We just found out the hard way.

**Q: Can I run this on n8n Cloud?**
A: Sure. But the localhost URLs in this README (and any hardcoded
`localhost:5678` references) will need adjusting. Also bring snacks for the
API rate limits.

**Q: Why 95 and not 100?**
A: Because the LLM scoring another LLM's resume at a perfect 100 every time
would mean one of them is broken. 95 is aspirational but reachable.

---

## 20. License & Disclaimers (Lawyer-Approved Cynicism) ⚖️

- **License:** WTFPL with a side of "don't blame us if you get rejected."
  Actually, no formal license — it's your workflow now. Do what you want.
  (But see next bullet.)
- **Disclaimer:** This workflow may, at any time, produce invalid LaTeX,
  hallucinate a JD, spam your Telegram, or loop until your CPU begs for mercy.
  We accept no liability for hiring outcomes, broken keyboards, or existential
  crises triggered by watching your before-score.
- **A note on automation:** Auto-optimizing applications at industrial scale
  is a thing. Use responsibly. The ATS may eventually learn. We'll deal with
  that in v2. 🦾

---

## 21. Changelog (The Scar Tissue) 📜

### v1dcf808c — "The Name Is The Game" 🏷️
- `filename` in `Prepare compilation ready` is now **candidate name only**
  (no `_Resume.pdf` suffix).
- `Build Caption + Cover Letter` derives `resumeFilename` (`.pdf`) and
  `coverLetterFilename` (`.html`) from that base.
- Telegram nodes append `_resume.pdf` / `_coverletter.html` at send time.
- Caption `📄 File:` line now shows the full resume filename.
- **Fixed:** `settings` on PUT stripped to `{ executionOrder }` only.

### v55a7a685 — "The Newline Heist" 📝
- Fixed the `---# ATS OPTIMIZATION RULES` header being glued to the previous
  line (a missing newline made the REBUILD MODE comment invisible).
- Re-PUT via no-BOM body + `curl.exe --data-binary`.

### v20a5110f — "The Loop Tightens" 🔁
- REBUILD MODE block added to writer prompt (`{% if $json.iteration > 1 %}`).
- `MAX_ITERATIONS = 10` in both `ATS Loop Guard` and `ATS Check`.
- Temperatures tuned (0.2/0.5/0.6 across the six model nodes).
- Workflow activated.

### v1 (origin) — "Let There Be ATS" ✨
- 23 nodes of optimistic resume juice, imported from a copy of
  "OptimizeResumeAsPerJD — Enhanced."

---

## 👤 Author

**Nitin Kumar**
🔗 [LinkedIn](https://www.linkedin.com/in/nitinkumar)
🔗 [GitHub](https://github.com/nitinkumar30)

> Built with ☕, too many LaTeX error logs, and the firm belief that your resume
> should work as hard as you do.

---

## 🎉 Final Words

You now possess the complete, unvarnished truth about this workflow. It loops.
It scores. It yells at LLMs. It delivers PDFs. It occasionally loses its mind
and writes broken LaTeX. But when it works — and it does work — it turns a
mediocre resume into a keyword-saturated, ATS-approved, Telegram-blessed
document of pure ambition. 🚀

Go forth. Score 95. Change careers. Buy a treadmill. We believe in you. 💪

*— The Maintainer(s) Who Definitely Commented Every Line of This, Probably*
