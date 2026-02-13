---
description: "Merge two VOC items into one, transferring all relationships and creating AI-suggested combined content."
---

# Merge VOC Items

Walk the user through merging two VOC items.

## Workflow

1. **Get the two items** — Ask for IDs or help the user search using `find_similar_voc_items` or `search_voc_items`
2. **Preview the merge** — Call `suggest_merge` and show the recommendation: which item survives, suggested merged content, and relationships to transfer
3. **Confirm target and content** — Let the user swap target/source or edit the merged title, description, and feature request
4. **Execute** — Call `execute_merge` with the confirmed parameters
5. **Confirm** — Show the merged result with a link to the target item
