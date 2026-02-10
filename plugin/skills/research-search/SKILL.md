---
description: "Search and browse GTM research packs, read report content, and check research request status."
---

# Research Search & Discovery

Answer questions about account research using these tools:

- **"Show me all research packs"** → `list_research_packs`
- **"What research exists for [company]?"** → `list_research_packs` with company filter
- **"Show me the fingerprint for [company]"** → `get_research_report` with report_type=fingerprint
- **"Read the AE briefing for [slug]"** → `get_research_report` with report_type=ae_briefing
- **"What research requests are pending?"** → `list_research_requests`
- **"Show completed requests"** → `list_research_requests` with status=completed
- **"Browse research packs"** → Read the `gtm://research-packs` resource

Use `generate_research` prompt for end-to-end research generation workflows.
