# vision-toolbox

Universal file analyzer — send images, PDFs, videos, Office documents, and code files to NVIDIA's free multimodal API for analysis.

## Quick Start

```bash
uv sync
export NVIDIA_API_KEY=nvapi-...
uv run vision photo.jpg
uv run vision document.pdf --prompt "extract all text"
uv run vision meeting.mp4 --prompt "summarize what happened"
uv run vision report.docx data.csv --prompt "analyze the business data"
```

## How It Works

```
file → classify → convert → NVIDIA API → text response

image  → base64              ──┐
video  → ffmpeg key frames   ──├── Kimi K2.5 / Qwen VL → analysis
pdf    → fitz render         ──┤
office → python-docx/openpyxl ──┘
text   → direct read         ──┘
```

## Setup

1. Get free API key at [build.nvidia.com](https://build.nvidia.com)
2. `uv sync`
3. `export NVIDIA_API_KEY=nvapi-...`
4. Done

## License

MIT
