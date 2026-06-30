---
document:
  id: STD-001
  title: Documentation Standard
  project: DevStorm Portfolio Platform
  version: 1.0.0
  status: Approved
---

# Documentation Standard

## Purpose

This document defines the documentation conventions followed throughout the DevStorm Portfolio Platform.

---

# Directory Structure

```text
docs/
├── phase-0/
├── standards/
├── architecture/
├── api/
├── database/
├── adr/
├── reports/
└── assets/
```

---

# File Naming Convention

Use lowercase with hyphens.

Example

```
0.1-product-vision.md

system-architecture.md

commit-conventions.md
```

---

# Document Metadata

Every document must start with:

```yaml
---
document:
  id:
  title:
  version:
  status:
---
```

---

# Heading Convention

```
# Title

## Section

### Subsection

#### Details
```

---

# Tables

Use tables whenever information can be compared.

Example

| Item | Description |
|------|-------------|

---

# Images

Store inside

```
docs/assets/
```

Never mix images with markdown files.

---

# Requirement IDs

Examples

```
FR-001

NFR-001

ADR-001

API-001
```

---

# Status Values

- Draft
- Review
- Approved
- Deprecated

---

# Markdown Rules

- One H1 per document
- Blank line between sections
- Use fenced code blocks
- Use relative paths

---

# Review Checklist

Before committing:

- Grammar checked
- Naming correct
- Metadata present
- Tables aligned
- Links verified

---

# Version History

| Version | Description |
|----------|-------------|
| 1.0.0 | Initial documentation standard |