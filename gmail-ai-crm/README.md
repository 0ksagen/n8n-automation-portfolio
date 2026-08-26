# Gmail AI CRM

An n8n portfolio project for automatically processing incoming emails, extracting structured information and routing messages according to business rules.

## Problem

Incoming business emails can contain orders, leads, questions or unrelated messages.

Manually reviewing every email, extracting customer information and copying it into a CRM or spreadsheet is repetitive and error-prone.

The goal of this workflow was to automate that process while keeping the final business decision deterministic.

## Workflow

```mermaid
flowchart LR
    A[Gmail Trigger] --> B[Get Message]
    B --> C[Normalize Fields]
    C --> D[AI Structured Extraction]
    D --> E[Business Validation]
    E --> F{Switch}
    F --> G[ORDER]
    F --> H[LEAD]
    F --> I[QUESTION]
    F --> J[OTHER]
    G --> K[Google Sheets]
    H --> K
    I --> K
