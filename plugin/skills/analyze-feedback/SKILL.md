---
description: "Analyze unstructured customer feedback (meeting notes, transcripts, emails) and extract actionable VOC items. Matches to existing items or proposes new ones."
---

# Analyze Feedback

Use the `analyze_feedback` prompt to guide this workflow, or follow these steps:

1. **Get the feedback** — Ask the user to paste meeting notes, transcripts, or emails
2. **Parse** using `parse_feedback` with optional company_id for context
3. **Review proposals** — Show each extracted item with match status (existing vs new)
4. **Execute with approval** — Create new items with `create_voc_item` or link to existing with `add_company_to_voc_item`
5. **Summarize** — Show a table of all actions taken
