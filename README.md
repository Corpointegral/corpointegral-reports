# corpointegral-reports

Daily market report published by the "Informe Financiero Diario" Grok automation
(grok.com/automations), and consumed by the `summer-art-70b1corpointegral-analytics`
Cloudflare Worker that serves `analytics.corpointegral.net`.

## `latest.json`

Overwritten once a day, around 9:00 AM ET, by Grok's GitHub connector. Shape:

```json
{
  "date": "YYYY-MM-DD",
  "dateLabel": "Human-readable date in Spanish, e.g. \"martes, 15 de septiembre de 2026\"",
  "html": "The report body as clean HTML (inner content only, no <html>/<body> tags)",
  "generatedAt": "ISO 8601 timestamp of when the report was generated"
}
```

The Cloudflare Worker fetches this file on its own daily cron and copies it into
KV (`REPORTS` namespace) under `latest` and `report-<date>`, exactly like it used
to do after calling the Anthropic API directly — the only thing that changed is
the source of the content.
