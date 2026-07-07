# Tableau Scribe

**Auto-documentation and metric dictionary engine for Tableau, powered by MCP.**

Tableau Scribe connects to your Tableau Cloud or Server environment via the [Tableau MCP](https://github.com/tableau/tableau-mcp) and generates polished, audience-ready documentation from live views and datasources — no screenshots, no manual data entry, no copy-paste.

---

## What It Does

Tableau Scribe operates in two modes:

### Mode 1: Auto-Doc Generator

Point it at any published Tableau view and receive structured dashboard documentation covering purpose, key metrics, filters, usage guidance, and a lightweight design health summary. The skill fetches the rendered image, view metadata, workbook context, and datasource schema automatically.

### Mode 2: Metric Definition Builder

Point it at any published datasource and receive a metric dictionary with plain-language definitions, directionality, business context, and field classifications. Designed so business users can understand what each metric means without opening Tableau.

---

## Key Features

- **Two depth levels** — Brief (1-page reference card) or Detailed (full 3-page documentation)
- **Three output formats** — `.docx` (Word), on-screen (inline markdown), or `.md` (downloadable file)
- **Zero-upload workflow** — No screenshots needed; MCP pulls the view image and metadata directly
- **Graceful degradation** — If an API call fails (401, timeout, permission issue), Scribe still produces what it can and explains gaps in a bottom note rather than aborting
- **Inline detection** — If you specify format or depth in your request ("give me a brief Word doc"), Scribe skips the questions and goes straight to work
- **Stale metadata detection** — Flags when datasource schema and rendered view are out of sync
- **Execution time transparency** — Tells you upfront how long to expect (~15s brief, ~30-60s detailed)

---

## Prerequisites

1. **Claude Desktop** with agent mode enabled
2. **Tableau MCP** configured and authenticated against your Tableau Cloud or Server site
3. **Permissions** — Your Tableau user needs at least Viewer access to the views/datasources you want to document

---

## Usage

Trigger Tableau Scribe with natural language:

```
Document this dashboard: [view name or URL]
```

```
Generate a metric dictionary for [datasource name]
```

```
/tableau-scribe
```

### Example Prompts

| Prompt | Mode | What Happens |
|--------|------|--------------|
| "Document the Sales Overview dashboard as a Word doc" | Auto-Doc | Detects .docx format, asks depth, generates documentation |
| "Give me a brief metric dictionary for the Segment Consumption datasource" | Metric Builder | Detects brief depth, asks format, generates dictionary |
| "Write detailed documentation for this view on screen" | Auto-Doc | Skips both questions (format + depth detected), proceeds immediately |
| "Tableau scribe — document everything about my Data Cloud dashboard" | Auto-Doc | Detects detailed depth, asks format |

---

## Output Structure

### Auto-Doc (Brief)

A single-page quick reference: purpose, top metrics with directionality, filters, how-to-read guidance, and refresh notes.

### Auto-Doc (Detailed)

Seven sections: Purpose & Audience, Key Metrics (with definitions, business meaning, and directionality), Filters & Interactivity, How to Use This Dashboard, Data & Refresh, Design Health Summary, and Glossary.

### Metric Dictionary (Brief)

Table-based one-liners: measures, calculated fields, and parameters — one row each with definition and direction.

### Metric Dictionary (Detailed)

Full field-level documentation: primary measures with business context and typical ranges, calculated fields with plain-language logic explanations, dimensions with cardinality, date fields with granularity, parameters with allowable values, and field relationship notes.

---

## Skill Ecosystem

Tableau Scribe is designed to work alongside other Tableau MCP skills:

```
Blueprint ──→ Build ──→ Scribe ──→ VizCritique
(design)      (create)   (document)   (evaluate)
```

| Skill | Relationship |
|-------|-------------|
| **Tableau Dashboard Blueprint** | Designs the dashboard → Scribe documents what was built |
| **Tableau Calc Master** | Writes calculations → Scribe explains them in plain language |
| **Tableau Auto-Query** | Provides sample data → Scribe uses it to enrich metric definitions |
| **VizCritique Pro** | Full scored evaluation → Scribe includes only a lightweight health summary and defers to VizCritique for depth |

---

## Error Handling Philosophy

Scribe never aborts because one API call failed. Instead:

1. It produces documentation from whatever data is available (graceful degradation across 5 priority levels)
2. It places a **bottom note** at the end of the document explaining what was unavailable and why — keeping the documentation body clean
3. It marks individual fields with "(inferred)" or "(not currently visible)" when specific items can't be confirmed

This means you always get output, even when your Tableau session has expired or a datasource is permission-restricted.

---

## Version History

| Version | Changes |
|---------|---------|
| v1.3 | Depth question previews, execution time expectations, stale metadata detection |
| v1.2 | Brief/Detailed depth modes, bottom-note error pattern, format question upfront, inline detection |
| v1.1 | Structural enhancements from independent scoring |
| v1.0 | Initial release — dual-mode Auto-Doc + Metric Builder |

---

## Author

**Adam Mico** — Built on the documentation methodology from [Dashboard Documentation Pro](https://chatgpt.com/g/g-6796e3b1e8a08191a7a2c2c20b2d22c7-dashboard-documentation-pro-by-adam-mico), adapted for the Tableau MCP ecosystem.

---

## License

This skill is provided as-is for use within the Claude Desktop agent environment. See your organization's Tableau MCP licensing for API access terms.

