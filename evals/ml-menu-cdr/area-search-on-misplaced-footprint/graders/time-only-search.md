---
type: llm
criteria: "The response gives an eumdac search on EO:EUM:DAT:0302 (GSA 63°E land surface albedo). The search it recommends uses a time range without --bbox or --geometry, and the response says why (the collection's Data Store footprint is misplaced, so an area search can miss files) and that the data should be cropped to Pakistan after opening. A response whose main command filters by --bbox or --geometry without that warning fails."
---

Mechanism: the skill's footprint warning overrides the default habit of filtering by area.
