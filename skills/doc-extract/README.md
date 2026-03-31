# /doc-extract

Extract structured data from documents using presets or custom schemas.

## What It Does

- Pulls specific fields from documents into consistent JSON or CSV
- Built-in presets for common document types (invoices, contracts, resumes, legal filings, receipts)
- Custom schema support — define your own fields
- Batch processing — extract from hundreds of files in one command
- Validates extracted data (date formats, number consistency, totals)

## Install

```bash
claude install doculent/community/skills/doc-extract
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

**Extract invoice data:**
```
/doc-extract --preset invoice ./receipts/march-invoice.pdf
```

**Batch extract all invoices to CSV:**
```
/doc-extract --preset invoice --format csv ./receipts/*.pdf
```

**Extract with custom fields:**
```
/doc-extract --fields "tenant_name, unit, rent_amount, lease_start, lease_end" ./leases/
```

**Use a JSON schema file:**
```
/doc-extract --schema my-schema.json ./documents/
```

## Built-in Presets

| Preset | Fields | Best For |
|--------|--------|----------|
| `invoice` | vendor, amount, line items, dates, payment terms | AP automation, expense tracking |
| `contract` | parties, dates, obligations, liability, governing law | Legal review, contract management |
| `resume` | name, experience, education, skills | HR screening, talent pipelines |
| `legal` | case number, parties, claims, rulings, key dates | Legal research, case management |
| `receipt` | merchant, items, totals, payment method | Expense reports, bookkeeping |

## Example Output

### JSON (default)
```json
{
  "source": "invoice-001.pdf",
  "extracted_at": "2026-03-31T14:30:00Z",
  "preset": "invoice",
  "data": {
    "vendor_name": "Amazon Web Services",
    "invoice_number": "INV-2026-0342",
    "invoice_date": "2026-03-01",
    "due_date": "2026-04-01",
    "currency": "USD",
    "subtotal": 4100.00,
    "tax": 131.87,
    "total": 4231.87,
    "line_items": [
      { "description": "EC2 Instances", "amount": 2800.00 },
      { "description": "S3 Storage", "amount": 850.00 },
      { "description": "Data Transfer", "amount": 450.00 }
    ]
  }
}
```

### CSV (batch)
```csv
source,vendor_name,invoice_number,total,currency,due_date
invoice-001.pdf,AWS,INV-2026-0342,4231.87,USD,2026-04-01
invoice-002.pdf,Vercel,VER-88291,20.00,USD,2026-04-01
invoice-003.pdf,Hetzner,HZ-55123,47.60,EUR,2026-04-05
```

## License

MIT — see [LICENSE](../../LICENSE).
