# Quick Start Prompts

## EUMDAC

```text
Help me install EUMDAC safely and verify the CLI.
```

```text
Write a safe EUMDAC credential setup checklist.
```

```text
Show me how to search an EUMETSAT Data Store collection with EUMDAC.
```

```text
Create a Python EUMDAC example that lists collections and downloads one product.
```

```text
Help me inspect EUMDAC Data Tailor options before customizing a product.
```

## EWCCLI

```text
Help me install EWCCLI safely and verify the ewc command.
```

```text
Write a safe EWC login profile setup checklist.
```

```text
Show me how to list and inspect EWC Community Hub items.
```

```text
Help me dry-run an EWC Community Hub deployment.
```

```text
Check a custom EWC Hub catalogue before deployment.
```

## Firecube

```text
Help me install Firecube from PyPI and verify the CLI.
```

```text
I have NetCDF files in a directory and an installed Firecube plugin. Plan a safe ingestion run to a local Zarr target.
```

```text
Scaffold a new Firecube plugin for my dataset and explain which ingestor template to pick.
```

```text
My Firecube ingestion crashed halfway. Show me how to inspect chunk records and recover safely.
```

```text
Benchmark and tune a Firecube ingestion: batch size, parallel slots, and storage driver.
```

## ESF Satellite Data

These prompts require an ESF MCP connection supplied by your service administrator.

```text
Use esf-satellite-data to select 100 distinct storm events and plan matching satellite imagery.
I have not chosen a time range, region, or output format. Do not transfer data yet.
```

## Feature DB Client

These prompts require an authorized Feature Database endpoint and the separately distributed client package.

```text
Use feature-db-client to write a read-only feature query for my configured endpoint.
Load credentials from the environment and do not print them. Do not execute writes.
```

## Climate Data Records

These prompts need no credentials until you search or download through the eumdac skill.

```text
Use ml-menu-cdr to tell me which EUMETSAT record gives monthly surface albedo over West Africa since 2000,
and which files and variable to use. Do not download anything.
```
