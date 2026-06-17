---
name: paddleocr-text-recognition
description: >-
  Use this skill whenever the user wants text extracted from images, photos, scans, screenshots,
  or scanned PDFs. Returns exact machine-readable strings with line-level text and optional bbox
  coordinates. Strong accuracy for CJK, small print, and handwritten text.
  Trigger terms: OCR, 文字识别, 图片转文字, 截图识字, 提取图中文字, 扫描识字, 识字, 纯文字,
  plain text extraction, 坐标, 检测框, bbox, bounding box, image to text, screenshot, photo scan,
  recognize text.
license: Apache-2.0
compatibility: opencode
metadata:
  requires:
    env:
      - PADDLEOCR_ACCESS_TOKEN
    bins:
      - paddleocr
  emoji: "🔤"
  install:
    - kind: pip
      package: paddleocr
      bins: [paddleocr]
---
# PaddleOCR Text Recognition

## When to Use This Skill

**Use this skill for**:
- Extract text from images (screenshots, photos, scans)
- Extract text from PDFs or document images when the goal is **line/box-level text**
- Extract text from URLs or local files that point to images/PDFs

**Do not use for**:
- Documents with tables, formulas, charts, or complex layouts — use Document Parsing instead

## Prerequisites

1. Install PaddleOCR CLI:
   ```bash
   pip install paddleocr
   ```

2. Get an API token from https://www.paddleocr.ai and set it:
   ```bash
   set PADDLEOCR_ACCESS_TOKEN=your_token_here
   ```

## Usage

### Basic OCR

From URL:
```bash
paddleocr api --model_type ocr --file_url "https://example.com/image.png"
```

From local file:
```bash
paddleocr api --model_type ocr --file_path "./document.png"
```

### Common Options

```bash
# With specific model
paddleocr api --model_type ocr --model PP-OCRv5 --file_path "./report.pdf"

# Disable preprocessing (faster, for flat images)
paddleocr api --model_type ocr --file_path "./document.pdf" --use_doc_unwarping False --use_doc_orientation_classify False

# Save result to file
paddleocr api --model_type ocr --file_url "https://..." --output result.json

# Page ranges for PDFs
paddleocr api --model_type ocr --file_path "./large.pdf" --page_ranges "1-5,10,15-20"
```

### Output Format

```json
{
  "pages": [
    {
      "prunedResult": {
        "rec_texts": ["Line 1", "Line 2"],
        "rec_scores": [0.98, 0.95]
      },
      "ocrImageUrl": "https://..."
    }
  ]
}
```

## Important Notes

- **Display complete results**: Always show the full extracted content. Do not truncate with "..." unless content exceeds 10,000 characters.
- **Handle errors gracefully**: When the CLI returns an error, inform the user of the specific issue.
- **Preprocessing**: Enabled by default. Disable for flat, well-oriented images (screenshots, properly scanned docs) for faster results.
