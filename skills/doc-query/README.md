# /doc-query

Ask questions across multiple documents. Get cited answers.

## What It Does

- Indexes a collection of documents (PDFs, markdown, text, images)
- Answers questions by searching across all indexed documents
- Cites specific documents, sections, and page numbers for every answer
- Flags contradictions between documents automatically
- Supports aggregation queries ("total budget", "earliest deadline")
- Works as an interactive session for follow-up questions

## Install

```bash
claude install doculent/community/skills/doc-query
```

### Dependencies

- `poppler-utils` — for PDF processing
- `tesseract` — for scanned document OCR (optional)

```bash
# macOS
brew install poppler tesseract

# Ubuntu/Debian
apt install poppler-utils tesseract-ocr
```

## Usage

**Ask a question about a folder of documents:**
```
/doc-query ./project-docs/ "Which document mentions API rate limits?"
```

**Start an interactive session:**
```
/doc-query ./contracts/
> What's the total value across all contracts?
> Which contract has the earliest termination date?
> Show me all non-compete clauses
```

**Query a specific set of files:**
```
/doc-query ./spec.pdf ./guide.pdf ./readme.md "How does authentication work?"
```

## Example Output

```markdown
## Answer

Rate limits are mentioned in 2 documents, but they disagree on the threshold.

### Sources

- **technical-spec.md**, Section 4.3 (Rate Limits):
  > "Each API key is limited to 1,000 requests per minute.
  > Exceeding this limit returns HTTP 429."

- **integration-guide.pdf**, Page 12:
  > "Clients exceeding 500 requests per minute will receive
  > 429 Too Many Requests responses."

### Contradictions

⚠ Rate limit values differ: 1,000 req/min (technical-spec.md)
  vs 500 req/min (integration-guide.pdf). Verify which is current.
```

### Aggregation Example

```
> What's the total budget across all SOWs?

| Document         | Budget   |
|------------------|----------|
| sow-frontend.pdf | $85,000  |
| sow-backend.pdf  | $120,000 |
| sow-infra.pdf    | $45,000  |

**Total: $250,000**
```

## How It Works

1. Discovers and reads all documents in the provided path
2. Chunks each document by sections/headings/pages
3. Searches chunks for terms relevant to your question
4. Reads the most relevant sections in full
5. Synthesizes an answer with citations
6. Cross-checks for contradictions between sources

## License

MIT — see [LICENSE](../../LICENSE).
