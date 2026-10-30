---
name: prefix-filter-before-search
description: A request for one product of a collection that holds every product and time step must filter on the filename prefix and time-step code. Fixture: user asks for monthly surface incoming shortwave radiation over Germany.
tags: [ml-menu-cdr, filtering, routing]
runs: 3
max_turns: 8
timeout_seconds: 300
---

Get me monthly surface solar radiation over Germany for 2015 to 2020 from EUMETSAT. Just tell me what to search for, don't download anything.
