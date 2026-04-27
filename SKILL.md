---
name: vision
description: Analyze images, PDFs, videos, Office documents, and code files via NVIDIA free multimodal API. Use when the user sends an image or non-text file that needs analysis — OCR, visual description, document extraction, video frame analysis. Invoke with file path(s).
---

# Vision Toolbox — Non-text Content Analyzer

Analyze any non-text file using NVIDIA's free multimodal API (Kimi K2.5, Qwen3.5 VL, etc.).

## Usage

```bash
# Single image
uv run vision image.jpg

# PDF (auto-rendered as images)
uv run vision document.pdf

# Video (auto-extracted key frames)
uv run vision video.mp4

# Office doc (auto-extracted text)
uv run vision report.docx

# Multiple files, custom prompt
uv run vision img1.jpg img2.jpg --prompt "compare these two screenshots"

# Choose model
uv run vision image.jpg --model qwen/qwen3.5-397b-a17b
```

## Supported Formats

| Category | Extensions | Method |
|----------|-----------|--------|
| Images | jpg, png, gif, webp, bmp, tiff | base64 → VLM |
| PDF | pdf | fitz render → image → VLM |
| Video | mp4, avi, mov, mkv, webm | ffmpeg key frames → VLM |
| Office | docx, xlsx, pptx | text extraction → VLM |
| Text | py, js, json, csv, md, html... | direct read → VLM |

## Prerequisites

1. NVIDIA API key (free): register at https://build.nvidia.com
2. Set `NVIDIA_API_KEY` env var or pass `--key nvapi-xxx`
3. Python ≥ 3.11 + `uv` (or pip install deps)
4. System tools: `ffmpeg` (for video), `tesseract` (for OCR, optional)

## Setup

```bash
uv sync
export NVIDIA_API_KEY=nvapi-...
uv run vision --list-models
uv run vision your-file.jpg
```

## Notes

- Free tier: 40 requests/min, no credit card required
- Video extracts max 8 frames at 5s intervals
- PDF renders max 5 pages at 150 DPI
- Text files capped at 80K chars
- API endpoint: `https://integrate.api.nvidia.com/v1` (OpenAI-compatible)
