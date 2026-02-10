---
description: "Generate account research: find pending requests, gather transcript intelligence, create reports, publish packs, and complete requests."
---

# Generate Account Research

Use the `generate_research` prompt to guide this workflow, or follow these steps:

1. **Find work** — Use `list_research_requests` to find pending requests, or ask the user which company to research
2. **Gather intelligence** — Use `query_transcripts` and `search_transcripts_semantic` for call data, `search_companies` for account details
3. **Generate reports** — Create Fingerprint Scorecard, AE Briefing, CS Briefing, or Full Pack based on request type
4. **Publish** — Use `publish_research_pack` with reports, company link, and assignees
5. **Complete** — Use `complete_research_request` to mark the request done and notify via Slack

## Report Types

| Type | Slug | Focus |
|------|------|-------|
| Fingerprint Scorecard | `fingerprint` | Company overview, ICP fit, competitive landscape |
| AE Briefing | `ae_briefing` | Talking points, objection handling, expansion opportunities |
| CS Briefing | `cs_briefing` | Health summary, risk factors, adoption gaps |
| Full Research Pack | `full_pack` | Comprehensive account analysis |
