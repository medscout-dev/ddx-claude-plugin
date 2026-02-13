---
description: "Analyze unstructured customer feedback (meeting notes, transcripts, emails) and extract actionable VOC items. Matches to existing items or proposes new ones."
---

# Analyze Feedback

Use the `analyze_feedback` prompt to guide this workflow, or follow these steps:

1. **Get the feedback text** from the user (meeting notes, transcript excerpt, email, etc.)
2. **Identify the company** if mentioned, using `search_companies`
3. **Parse the feedback** using `parse_feedback` to extract structured items with match proposals
4. **Present proposals** to the user:
   - Existing matches: show the matched item, similarity score, and URL
   - New items: show the proposed title and problem statement
5. **Let the user edit** — for each proposal, the user can approve as-is, edit fields, or skip
6. **Execute approved proposals**: create new items with approved content, or add companies to existing ones
7. **Summarize** all actions taken with links to created/updated items
