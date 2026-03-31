# /doc-parse

Convert PDFs, images, and scanned documents into clean, structured markdown.

## What It Does

- Extracts text from PDFs (text-based and scanned)
- Performs OCR on images and scanned documents
- Detects and preserves document hierarchy (headings, sections, subsections)
- Converts tables into proper markdown tables
- Adds metadata frontmatter (author, date, page count)
- Generates a table of contents for long documents
- Handles large documents by chunking intelligently

## Install

```bash
claude install doculent/community/skills/doc-parse
```

### Dependencies

- `poppler-utils` — for PDF processing (`pdftotext`, `pdftoppm`)
- `tesseract` — for OCR on images and scanned PDFs

```bash
# macOS
brew install poppler tesseract

# Ubuntu/Debian
apt install poppler-utils tesseract-ocr
```

## Usage

**Parse a single PDF:**
```
/doc-parse ./contracts/vendor-agreement.pdf
```

**Parse a scanned image:**
```
/doc-parse ./scans/receipt.png
```

**Parse all PDFs in a directory:**
```
/doc-parse ./legal-documents/
```

## Example Output

```markdown
---
source: vendor-agreement.pdf
pages: 47
author: Legal Team
created: 2026-01-15
parsed: 2026-03-31
---

# Vendor Agreement — Acme Corp ↔ Doculent Ltd

## Table of Contents
1. [Definitions](#1-definitions)
2. [Scope of Services](#2-scope-of-services)
3. [Payment Terms](#3-payment-terms)
...

## 3. Payment Terms

| Milestone | Amount   | Due Date   |
|-----------|----------|------------|
| Signing   | $25,000  | 2026-04-01 |
| Delivery  | $50,000  | 2026-06-15 |
| Final     | $25,000  | 2026-08-01 |
```

## How It Works

1. Detects whether the PDF contains extractable text or is scanned
2. Uses `pdftotext` for text PDFs, `tesseract` for scanned pages
3. Analyzes the extracted text for structural patterns (headings, tables, lists)
4. Transforms into clean, well-structured markdown
5. Adds metadata and table of contents

## License

MIT — see [LICENSE](../../LICENSE).
