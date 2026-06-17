---
name: image-recognition
description: |
  Analyze images, screenshots, UI designs, charts, tables, and other visual content. Use when user asks "这是什么图片", "分析截图", "识别图片", "提取图中的文字", "OCR", "看这张图", "UI分析", or pastes an image path. Supports OCR, table extraction, chart data extraction, screenshot/UI analysis.
license: MIT
compatibility: opencode
metadata:
  audience: developers
  category: vision
---

# Image Recognition

Analyze local images using the model's built-in vision capabilities.

## When to Use

- User shares a screenshot or image path and asks what it shows
- User asks "分析这张截图/设计图/图表"
- User needs OCR / text extraction from an image
- User wants to extract data from a chart or table image
- User pastes a UI design mockup and asks for analysis
- User uploads a screenshot of an error and wants diagnosis

## How to Use

### Step 1: Read the image

Use the `read` tool on the image file path. OpenCode automatically handles image attachments and sends them to the model (for vision-capable models).

### Step 2: Analyze based on request type

**General image analysis:**
- Describe the image content in detail
- Identify key elements, text, colors, layout
- Note any important details relevant to the user's question

**Screenshot / UI analysis:**
- Identify the type of interface (web page, mobile app, desktop app, terminal)
- Describe the layout: header, navigation, content areas, footer
- List UI components: buttons, forms, tables, cards, modals
- Note colors, typography, spacing patterns
- Identify any issues: alignment problems, missing elements, accessibility concerns

**OCR / text extraction:**
- Extract all visible text from the image
- Preserve the original layout and grouping
- Note any text that is cut off or unclear

**Chart / table data extraction:**
- Identify the chart type (bar, line, pie, etc.)
- Extract data points with labels and values
- For tables: extract rows and columns as structured data

**Error screenshot analysis:**
- Extract the error message text
- Note the context (which app, which page)
- Identify error codes, stack traces, or logs

### Step 3: Provide actionable results

Return the analysis in a structured format appropriate to the request type. For UI analysis, focus on aspects relevant to the user's project (e.g., if they're building a web app, analyze component structure and layout patterns).
