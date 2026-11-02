---
type: llm
criteria: "The response asks the user for a maintainer contact (an email or a url for Alex Example) and for the catalog category, instead of inventing them. It does not fill in a made-up email address, a made-up maintainer url, or a guessed category value as if known; a clearly marked placeholder or a flagged omission is acceptable. Any YAML it drafts uses the item name sst-anomaly-tool as the exact key under spec.items and as the name attribute. Any deployment settings it drafts (main file, requirements file, image, security groups, inputs) sit under values.*, and it does not use the deprecated ewccli attributes pathToMainFile, pathToRequirementsFile, defaultImageName, defaultSecurityGroups or inputs (ewccli.externalIP and ewccli.checkDNS are fine). Technology is rendered as the schema value 'Ansible Playbook' and the license type as 'Apache License 2.0' if drafted."
---

Mechanism: skill rules 2 and 4 forbid inventing maintainer contacts and categories, rule 3 requires the spec.items key to equal name, and rule 6 prefers values.* over deprecated ewccli attributes. Pass only if the missing facts are requested, not fabricated.
