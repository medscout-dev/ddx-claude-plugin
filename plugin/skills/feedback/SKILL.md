---
description: "Submit feedback or a bug report about DDX directly to the #feedback-ddx Slack channel. Use when a user wants to report an issue or suggest an improvement."
---

# Submit DDX Feedback

Guide the user through submitting feedback about the DDX platform:

1. **Ask the type**: Is this a suggestion/improvement ("feedback") or a bug report ("bug")?
2. **Collect a description**: Ask the user to describe the feedback or bug in detail.
3. **Optionally ask which page or feature** it relates to (e.g. "VOC list", "Theme detail", "Transcript search").
4. **Call `submit_platform_feedback`** with the collected values. Pass the user's name or email as `submitted_by` if known.
5. **Confirm** the submission was successful and let the user know it was posted to #feedback-ddx.
