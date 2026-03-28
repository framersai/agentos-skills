---
name: document-export
version: '1.0.0'
description: Export research, reports, and analysis to PDF, DOCX, PPTX, CSV, and XLSX with professional formatting.
author: Wunderland
namespace: wunderland
category: productivity
tags: [document, export, pdf, docx, pptx, csv, xlsx, report, slides]
requires_secrets: []
requires_tools: [document_export, document_suggest]
metadata:
  agentos:
    emoji: "\U0001F4C4"
    homepage: https://wunderland.sh
---

# Document Export

You can export your responses, research, and analysis to professional documents.

## When to Offer Export

After generating substantive responses, use `document_suggest` to check if you should offer export:
- Long responses (500+ words) -> offer PDF or DOCX
- Data-heavy responses with tables -> offer CSV or XLSX
- Multi-section analysis -> offer PPTX slide deck
- Short conversational responses -> don't offer

## How to Export

When the user requests an export (or accepts your offer):
1. Structure your response content into DocumentContent format
2. Choose the right format based on what the user asked for
3. Call `document_export` with the structured content
4. Share the download link with the user

## Content Tips

- **PDF/DOCX reports**: Use level-1 heading for title, level-2 for sections. Include tables for data.
- **Slide decks**: Each major point becomes a section with layout hint. Use speakerNotes for talking points. Keep text concise.
- **CSV/XLSX**: Focus on tabular data. Each table becomes a sheet or CSV section.
- **Charts**: When data has categories + numeric values, add a chart spec. Bar for comparisons, line for trends, pie for composition.

## Theme Selection (PPTX)

- `corporate` -- business presentations, quarterly reviews
- `dark` -- tech demos, evening presentations
- `light` -- general purpose, academic
- `creative` -- marketing, product launches
- `minimal` -- data-focused, research

## Multi-Format

If the user says "export this" without specifying format, offer the most relevant options. Research -> PDF + DOCX. Data analysis -> XLSX + CSV. Presentation -> PPTX.
