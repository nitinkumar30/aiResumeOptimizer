# 🎬 Media Generation Guide — AI Resume Optimizer

This guide explains how to generate portfolio images & videos using the models integrated into the workflow.

## 🖼️ Image Generation Models

| Model | Best For | Prompt Style |
|-------|----------|-------------|
| **Google Gemini 2.5 Flash Image** | Fast portfolio images | Concise, technical |
| **Google Gemini 3 Pro Image** | High-quality hero banners | Detailed, artistic |
| **OpenAI GPT 5.4 Image-2** | Professional graphics | Structured, formal |
| **OpenRouter Auto** | Auto best-model routing | Any style |

## 🎬 Video Generation Models

| Model | Best For | Duration |
|-------|----------|----------|
| **xAI Grok Imagine Video** | Quick 10s portfolio clips | 10s |
| **Google Veo 3.1 Fast** | Fast preview videos | 15s |
| **Google Veo 3.1 Lite** | Lightweight shareable clips | 15s |
| **ByteDance Seedance 2.0 Fast** | Efficient quick renders | 10s |
| **Google Veo 3.1** | Full quality portfolio | 15-30s |
| **OpenAI Sora 2 Pro** | Studio-quality showcase | 15-60s |

## 📋 Prompt Templates

### Image Prompt
```
Professional LinkedIn banner for {Name}, a {Role} specialist.
Skills: {skill1}, {skill2}, ...
Style: clean, modern, tech-themed, blue gradient, 1200x600
```

### Video Prompt
```
Professional portfolio showcase video for {Name}, a {Role} professional.
{Skills}. 15 seconds, cinematic transitions, modern corporate style,
blue and white color scheme, animated text showing key achievements.
```

## 🔧 How to Use

1. Select "Yes — Images & Video" in the web form
2. Choose your preferred AI model
3. Submit resume + JD as usual
4. Media generates in parallel with the resume
5. Results delivered to Telegram alongside the PDF

## 📝 Notes

- API keys are required for each provider you want to use
- Media generation runs in parallel and doesn't slow down resume delivery
- If a model fails, the workflow gracefully handles the error
- Generated media is saved as base64 in the workflow output
