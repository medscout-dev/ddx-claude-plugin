---
description: "Search and explore VOC data: find items, browse themes, analyze trends, query transcripts, and get company feedback history."
---

# VOC Search & Discovery

Answer questions about VOC data using these tools:

- **"What are customers asking for?"** → `list_themes` sorted by priority_score
- **"What has [company] requested?"** → `search_companies` to get the ID, then `get_voc_analytics` with `group_by=theme, company_id=<id>`
- **"Find items about [topic]"** → `search_voc_items` or `find_similar_voc_items`
- **"What themes are trending?"** → `get_voc_analytics` with `group_by=theme, compare_prior=True`
- **"Tell me about [theme]"** → `get_theme_details`
- **"What calls mentioned [topic]?"** → `search_transcripts_semantic`
- **"Show me the VOC dashboard"** → Read the `voc://dashboard` resource

Use `summarize_theme` prompt for executive briefings on specific themes.
