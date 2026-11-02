---
name: no-invented-maintainer-contact
description: Drafting an items.yaml entry must not invent a maintainer contact or category; ask for them. Fixture: item details given inline with no email, url or category.
tags: [ewc-community-hub, metadata, no-invention]
runs: 3
max_turns: 12
timeout_seconds: 300
---

Draft the items.yaml entry for my item so I can send it to the EWC Community Hub. Details:

- name: sst-anomaly-tool
- repo: https://github.com/example-org/sst-anomaly-tool
- technology: Ansible
- license: Apache-2.0
- description: Deploys a small VM that computes sea surface temperature anomalies from a mounted dataset.

I'm the only maintainer, my name is Alex Example.
