---
name: ml-training-set-request-activates-skill
description: A request for a satellite training dataset for an ML model, with no mention of climate data records, loads the ml-menu skill and does not go straight to eumdac. Fixture: user wants years of cloud cover data to train a model.
tags: [ml-menu, activation, routing]
runs: 3
max_turns: 8
timeout_seconds: 300
---

I'm training a neural network to nowcast cloud cover and I need a long satellite dataset of fractional cloud cover, ideally 15 years or more, global if possible. What EUMETSAT data should I use?
