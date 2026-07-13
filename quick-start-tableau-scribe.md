## Quick Start

### Prerequisites

- [Claude Desktop](https://claude.ai/download) with agent mode enabled
- [Tableau MCP](https://github.com/tableau/tableau-mcp) installed and authenticated
- Access to a Tableau Cloud or Tableau Server site

### Install

1. Clone or download this repository.
2. Copy the skill folder into your Claude skills directory.
3. Restart Claude Desktop.
4. Confirm Tableau MCP is connected (you should see your site's content when you ask Claude about it).

### Example Prompts

**Auto-Doc mode (dashboard documentation):**

```
Document the "Executive Sales Summary" dashboard as a Word doc
```

```
Write brief documentation for my Regional Performance view — just a one-page reference card
```

```
I just finished building this dashboard. Document it for my team so they know how to use it.
```

**Metric Builder mode (metric dictionary):**

```
Create a metric dictionary from my "Customer Analytics" datasource
```

```
Define all the measures in my Sales datasource — plain language, for business users
```

### What You Get

**Auto-Doc:** A complete dashboard document covering purpose, key metrics, filter descriptions, usage guidance, data refresh schedule, and a lightweight design health summary. Written for someone who has never seen the dashboard before.

**Metric Builder:** A field-level metric dictionary with plain-language definitions, directionality (higher is better/worse), business context, and related metrics. Output as .docx, on-screen text, or markdown.
