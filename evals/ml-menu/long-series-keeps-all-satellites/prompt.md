---
name: long-series-keeps-all-satellites
description: A request for a long IASI ozone series gets the all-satellite filter, not a Metop-B-only one, and a note that the series spans Metop-A and Metop-B. Fixture: user wants to train a model on IASI ozone from 2008 to 2023.
tags: [ml-menu, long-series, filtering]
runs: 3
max_turns: 8
timeout_seconds: 300
---

I want to train a model on IASI ozone from 2008 to 2023. Which EUMETSAT files do I pull?
