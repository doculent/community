<h1 align="center">
  <br>
  <a href="https://doculent.io">
    <img src="https://doculent.io/images/iconDarkSVG.svg" alt="Doculent" width="80">
  </a>
  <br>
  Doculent Open Source
  <br>
</h1>

<h3 align="center">Free document intelligence tools for Claude Code.</h3>

<p align="center">
  <a href="https://doculent.io">Website</a> &bull;
  <a href="https://docs.doculent.io">Docs</a> &bull;
  <a href="https://discord.gg/VvqKKm2Ttz">Discord</a> &bull;
  <a href="https://github.com/doculent/community/discussions">Discussions</a>
</p>

<p align="center">
  <a href="#skills"><img src="https://img.shields.io/badge/Skills-5%20Available-blue?style=flat-square" alt="5 Skills"></a>
  <a href="https://github.com/doculent/community/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="MIT License"></a>
  <a href="https://discord.gg/VvqKKm2Ttz"><img src="https://img.shields.io/badge/Discord-Join-5865F2?style=flat-square&logo=discord&logoColor=white" alt="Discord"></a>
</p>

---

Open-source document intelligence tools from [Doculent](https://doculent.io). Parse, extract, compare, query, and redact documents — directly from your terminal using [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

These skills solve the problems LLMs can't handle alone: large documents that exceed context windows, batch processing across hundreds of files, consistent structured output, cross-document reasoning, and proper table extraction.

## Skills

<table>
  <thead>
    <tr>
      <th>Skill</th>
      <th>What It Does</th>
      <th>Use Case</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="./skills/doc-parse"><strong>/doc-parse</strong></a></td>
      <td>Convert PDFs and images into clean, structured markdown with tables, headings, and metadata</td>
      <td>Turn a 200-page contract into a searchable, version-controllable markdown file</td>
    </tr>
    <tr>
      <td><a href="./skills/doc-extract"><strong>/doc-extract</strong></a></td>
      <td>Pull structured data from documents using presets or custom schemas. Outputs JSON or CSV.</td>
      <td>Extract data from 50 invoices into a single CSV with one command</td>
    </tr>
    <tr>
      <td><a href="./skills/doc-compare"><strong>/doc-compare</strong></a></td>
      <td>Semantic diff between document versions — what changed, what it means, and what to watch</td>
      <td>Compare two contract versions and get a risk-rated change report</td>
    </tr>
    <tr>
      <td><a href="./skills/doc-query"><strong>/doc-query</strong></a></td>
      <td>Ask questions across multiple documents. Get cited answers with contradiction detection.</td>
      <td>Search 34 project documents for rate limit specs and find conflicting values</td>
    </tr>
    <tr>
      <td><a href="./skills/doc-redact"><strong>/doc-redact</strong></a></td>
      <td>Detect and redact PII — SSNs, emails, phones, addresses, credit cards, and more</td>
      <td>Strip personal data from 156 support tickets before sharing externally</td>
    </tr>
  </tbody>
</table>

## Quick Start

### Install

```bash
# Install all skills
claude install doculent/community

# Or install individually
claude install doculent/community/skills/doc-parse
claude install doculent/community/skills/doc-extract
claude install doculent/community/skills/doc-compare
claude install doculent/community/skills/doc-query
claude install doculent/community/skills/doc-redact
```

### Dependencies

These skills use standard document processing tools. Install once:

```bash
# macOS
brew install poppler tesseract

# Ubuntu / Debian
apt install poppler-utils tesseract-ocr

# Windows — see poppler and tesseract release pages
```

### Use

```bash
# Parse a PDF into structured markdown
/doc-parse ./contracts/vendor-agreement.pdf

# Extract invoice data to CSV
/doc-extract --preset invoice ./receipts/*.pdf

# Compare two contract versions
/doc-compare ./contract-v1.pdf ./contract-v2.pdf

# Ask questions across project documents
/doc-query ./project-docs/ "What's the total budget across all SOWs?"

# Redact PII from customer files
/doc-redact ./customer-data/intake-form.pdf
```

## Why Skills Instead of Raw Prompting?

LLMs can read documents. But they hit walls fast:

| Problem | What Happens | How Skills Fix It |
|---------|-------------|-------------------|
| Large documents | Models truncate or hallucinate past the context window | Skills chunk intelligently, process section by section |
| Inconsistent output | Same prompt, different JSON shape every time | Skills enforce schemas with validation |
| Multi-document queries | Can't fit 50 files in one prompt | Skills index, search, and retrieve relevant sections |
| Batch processing | Copy-paste one file at a time into ChatGPT | Skills process entire directories in one command |
| Table extraction | Models narrate tables as prose | Skills detect and output proper markdown/CSV tables |

These skills handle the orchestration layer — chunking, preprocessing, schema enforcement, batch processing — so the model focuses on understanding content, not managing logistics.

## What Is Doculent?

Doculent is an AI-powered document processing platform that turns fragmented files into structured business outcomes. We process 200 documents per minute at 99.2% extraction accuracy with human-in-the-loop verification.

**Built for high-volume operations** in insurance, healthcare, transportation, and freight.

These open-source skills are a distillation of the document intelligence techniques we use in production — made available for anyone working with documents in their development workflow.

<p align="center">
  <a href="https://doculent.io">Learn more at doculent.io</a>
</p>

## Project Structure

```
community/
├── skills/
│   ├── doc-parse/          # PDF/image → structured markdown
│   │   ├── SKILL.md
│   │   └── README.md
│   ├── doc-extract/        # Schema-based data extraction
│   │   ├── SKILL.md
│   │   └── README.md
│   ├── doc-compare/        # Semantic document diff
│   │   ├── SKILL.md
│   │   └── README.md
│   ├── doc-query/          # Multi-document Q&A
│   │   ├── SKILL.md
│   │   └── README.md
│   └── doc-redact/         # PII detection & redaction
│       ├── SKILL.md
│       └── README.md
├── CONTRIBUTING.md
├── SECURITY.md
└── LICENSE
```

## Contributing

We welcome contributions — new skills, improvements to existing ones, bug fixes, and documentation. See [CONTRIBUTING.md](./CONTRIBUTING.md) for the skill format and guidelines.

## Security

Found a vulnerability? See [SECURITY.md](./SECURITY.md). Do not open a public issue.

## License

MIT — see [LICENSE](./LICENSE).

---

<p align="center">
  <sub>Built by <a href="https://doculent.io">Doculent</a> — document intelligence for teams that deal with complex paperwork.</sub>
</p>
