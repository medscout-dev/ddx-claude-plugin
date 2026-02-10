---
description: "Submit a new VOC item to DDX. Searches for similar existing items first to avoid duplicates, then creates or matches."
---

# Submit VOC Item

Use the `submit_voc` prompt to guide this workflow, or follow these steps:

1. **Gather details** from the user: title, description, company, and any feature request
2. **Search for duplicates** using `find_similar_voc_items` with the description
3. **If similar items exist** (>0.70 similarity), show them and ask whether to add the company to an existing item or create new
4. **Resolve the company** using `search_companies` if a name was provided
5. **Create the item** with `create_voc_item` or update with `add_company_to_voc_item`
6. **Confirm** what was created with the item ID
