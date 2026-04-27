---
name: vision
description: Analyze images, PDFs, videos, Office documents, and code files via any OpenAI-compatible multimodal API. Use when the user sends an image or non-text file that needs analysis — OCR, visual description, document extraction, video frame analysis. Invoke with file path(s).
---

# Vision Toolbox — Non-text Content Analyzer

Analyze any non-text file using any OpenAI-compatible multimodal API.

## Usage

```bash
# Default: NVIDIA free API
uv run vision image.jpg

# Pick provider preset
uv run vision image.jpg --provider openai
uv run vision image.jpg --provider ollama
uv run vision image.jpg --provider openrouter

# PDF / Video / Office docs
uv run vision document.pdf
uv run vision video.mp4
uv run vision report.docx

# Custom endpoint
uv run vision image.jpg --base-url http://localhost:8080/v1/chat/completions --model llama-vision

# List all presets
uv run vision --presets
```

## Presets

| Preset | Endpoint | Default Model |
|--------|----------|---------------|
| `nvidia` | NVIDIA NIM (free) | Kimi K2.5 |
| `openai` | OpenAI API | GPT-4o |
| `ollama` | Local Ollama | llava |
| `lmstudio` | Local LM Studio | auto |
| `openrouter` | OpenRouter | GPT-4o |

## Supported Formats

| Category | Extensions | Method |
|----------|-----------|--------|
| Images | jpg, png, gif, webp, bmp, tiff | base64 → VLM |
| PDF | pdf | fitz render → image → VLM |
| Video | mp4, avi, mov, mkv, webm | ffmpeg key frames → VLM |
| Office | docx, xlsx, pptx | text extraction → VLM |
| Text | py, js, json, csv, md, html... | direct read → VLM |

## Setup

```bash
uv sync
export NVIDIA_API_KEY=nvapi-...   # for NVIDIA
# or
export OPENAI_API_KEY=sk-...      # for OpenAI
# or
export API_KEY=xxx                # generic (with --key flag)
```

## Notes

- All providers must be OpenAI-compatible (chat/completions endpoint)
- Anthropic (non-OpenAI-compatible) needs a proxy
- Video: max 8 frames at 5s intervals
- PDF: max 5 pages at 150 DPI
- Text files: capped at 80K chars
