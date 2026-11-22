---
name: stats
description: Show the user's WikiDrive usage counts. Run by the user as /wikidrive:stats, or used when the user asks how they use WikiDrive or how often a prompt is used.
argument-hint: "[optional: a topic or a prompt]"
disable-model-invocation: true
---

The user asked how they use WikiDrive.

1. Call `wikidrive_stats`, for the topic or prompt the user named if they named one.
2. Summarize the counts in a few short lines or a small table. Do not invent numbers; the result has counts only.

The `wikidrive` skill in this plugin has the details.
