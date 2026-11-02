---
name: validation-finds-schema-errors
description: Review of a pasted EWCCLI-compatible entry must find the key/name mismatch and the maintainer with no contact, must not certify validity by reading, and must add the custom-catalogue dry-run. Fixture: entry inline in the prompt.
tags: [ewc-community-hub, validation, schema]
runs: 3
max_turns: 12
timeout_seconds: 300
---

Is this valid? Can I submit it to the EWC Community Hub?

```yaml
apiVersion: communityhub.europeanweather.cloud/v1alpha1
kind: CommunityHubCatalog
spec:
  items:
    sst-tool:
      name: "sst-anomaly-tool"
      displayName: SST Anomaly Tool
      summary: Computes sea surface temperature anomalies
      description: |
        Deploys a small VM that computes sea surface temperature
        anomalies from a mounted dataset.
      version: "0.1.0"
      published: true
      home: https://github.com/example-org/sst-anomaly-tool
      license: https://github.com/example-org/sst-anomaly-tool/blob/main/LICENSE
      icon: https://raw.githubusercontent.com/example-org/sst-anomaly-tool/refs/heads/main/icon.png
      sources:
        - https://github.com/example-org/sst-anomaly-tool.git
      maintainers:
        - name: Alex Example
      annotations:
        category: "Compute"
        technology: "Ansible Playbook"
        licenseType: "Apache License 2.0"
        supportLevel: "Community"
        others: "Deployable,EWCCLI-compatible"
      values:
        inputSpec:
          - name: dataset_path
            description: "Path of the mounted dataset."
            type: str
        pathToMainFile: playbooks/sst.yml
```
