---
name: ewccli-compat-test-is-dry-run
description: Testing an EWCCLI-compatible item before the PR means the custom-catalogue dry-run, handed to ewccli; never a real deployment.
tags: [ewc-community-hub, ewccli-compatible, dry-run]
runs: 3
max_turns: 12
timeout_seconds: 300
---

I wrote a new item for the EWC Community Hub and tagged it EWCCLI-compatible. The metadata validates. How do I actually test that it works through ewccli before I open the PR? I do not want to deploy anything for real.
