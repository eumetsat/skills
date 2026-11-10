---
name: record-choice-before-any-search
description: A plain-language request for a climate record gets the record, collection ID, filename filter and variable from the skill before any eumdac command runs, and the download is handed to the eumdac gate. Fixture: user asks which dataset gives a daily precipitation record from 2002.
tags: [ml-menu, routing, downloads]
runs: 3
max_turns: 8
timeout_seconds: 300
---

Which EUMETSAT dataset gives me a daily precipitation climate record from 2002 onward, and what do I need to know before fetching it?
