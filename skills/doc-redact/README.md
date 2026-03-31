# /doc-redact

Detect and redact PII from documents.

## What It Does

- Scans documents for personally identifiable information (PII)
- Detects SSNs, emails, phone numbers, addresses, credit cards, dates of birth, names, and more
- Replaces PII with type-labeled placeholders (`[EMAIL-REDACTED]`, `[SSN-REDACTED]`, etc.)
- Generates a detailed scan report before redacting
- Supports selective redaction — choose which PII types to redact
- Batch processes entire directories

## Install

```bash
claude install doculent/community/skills/doc-redact
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

**Scan and redact a document:**
```
/doc-redact ./customer-data/intake-form.pdf
```

**Redact only specific PII types:**
```
/doc-redact --types email,phone ./support-tickets/
```

**Report only (no redaction):**
```
/doc-redact --output report ./documents/
```

**Batch redact a directory:**
```
/doc-redact ./hr-files/
```

## Example Output

### Scan Report
```
## PII Scan Results — intake-form.pdf

| # | Type    | Value              | Line | Confidence |
|---|---------|--------------------|------|------------|
| 1 | SSN     | 123-45-6789        | 12   | High       |
| 2 | Email   | john@example.com   | 15   | High       |
| 3 | Phone   | (555) 123-4567     | 16   | High       |
| 4 | Name    | John Michael Doe   | 8    | Medium     |
| 5 | Address | 123 Main St...     | 20   | Medium     |
| 6 | DOB     | 03/15/1990         | 24   | Medium     |

Summary: 6 PII instances (3 high confidence, 3 medium)
```

### Redacted Output
```
Patient Name: [NAME-REDACTED]
SSN: [SSN-REDACTED]
Date of Birth: [DOB-REDACTED]
Email: [EMAIL-REDACTED]
Phone: [PHONE-REDACTED]
Address: [ADDRESS-REDACTED]
```

## Detected PII Types

| Type | Detection | Confidence |
|------|-----------|------------|
| SSN | Regex pattern | High |
| Email | Regex pattern | High |
| Phone (US/Intl) | Regex pattern | High |
| Credit Card | Regex + Luhn check | High |
| IBAN | Regex pattern | High |
| IP Address | Regex pattern | High |
| Person Name | Context analysis | Medium |
| Physical Address | Multi-line pattern | Medium |
| Date of Birth | Context + date pattern | Medium |
| Bank Account | Context + number pattern | Medium |
| Driver's License | State patterns + context | Medium |
| Passport Number | Context + pattern | Medium |

## Important Notes

- Automated PII detection may miss non-standard formats — manual review is recommended for high-stakes documents
- PDF binary files cannot be modified directly — redacted output is a text/markdown version
- The scan report shows detected PII values to the user for verification — this data is not written to any external location

## License

MIT — see [LICENSE](../../LICENSE).
