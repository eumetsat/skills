# EWC VM Plans And Flavours

Use this reference when users ask which EWC flavours, flavors, plans, instance sizes, GPU plans, or HPC plans are available.

This snapshot is based on the official EWC Knowledge Base pages listed below. Both federee pages were last modified on 2026-04-20 when checked on 2026-04-29.

- EWC VM plans: https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+VM+plans
- ECMWF - VM plans and flavors: https://confluence.ecmwf.int/display/EWCLOUDKB/ECMWF+-+VM+plans+and+flavors
- EUMETSAT - VM plans and flavors: https://confluence.ecmwf.int/display/EWCLOUDKB/EUMETSAT+-+VM+plans+and+flavors

## Response Rules

1. Say that `ewccli 0.10.0` accepts a flavour with `ewc infra create --flavour-name <flavour-name>`, but does not provide a dedicated `ewc` command to list every available flavour.
2. Ask or infer the federee before recommending a flavour. ECMWF and EUMETSAT use different naming schemes.
3. Do not invent generic availability tables such as "small, medium, large, GPU". Use exact names from the official federee pages or point to the official pages.
4. Do not mix ECMWF and EUMETSAT flavour names in a command.
5. Mention that GPU, HPC, high-memory, and local-SSD plans may have access constraints when the official page says so.
6. Do not quote prices unless the user asks. If quoting prices, say they are from the dated official page snapshot and should be rechecked.

## EWCCLI Defaults

The inspected `ewccli 0.10.0` source uses these default CPU flavours:

| Federee / region | Default CPU flavour |
| --- | --- |
| ECMWF (CCI1, CCI2) | `4cpu-4gbmem-30gbdisk` |
| EUMETSAT (WAW3-1) | `eo1.large` |
| EUMETSAT (ECIS-R1, ECIS-R2) | `4cpu-4gbmem` |

These are defaults for `ewccli`, not the complete service catalogue.

## ECMWF Plans

Official page: https://confluence.ecmwf.int/display/EWCLOUDKB/ECMWF+-+VM+plans+and+flavors

General purpose:

```text
1cpu-1gbmem-30gbdisk
2cpu-2gbmem-30gbdisk
2cpu-4gbmem-30gbdisk
4cpu-4gbmem-30gbdisk
4cpu-8gbmem-40gbdisk
4cpu-16gbmem-40gbdisk
8cpu-8gbmem-30gbdisk
8cpu-16gbmem-80gbdisk
8cpu-32gbmem-80gbdisk
16cpu-16gbmem-30gbdisk
32cpu-32gbmem-30gbdisk
```

GPU plans are listed by the official page as available on request and subject to resource availability:

```text
8cpu-64gbmem-30gbdisk-a100.1g.10gbgpu
8cpu-64gbmem-30gbdisk-a100.2g.20gbgpu
16cpu-128gbmem-30gbdisk-40gbgpu
48cpu-384gbmem-30gbdisk-80gbgpu
```

High performance plans are listed by the official page as available on request and subject to resource availability:

```text
8cpu-32gbmem-30gbdisk-hpc
16cpu-64gbmem-30gbdisk-hpc
32cpu-128gbmem-30gbdisk-hpc
48cpu-192gbmem-30gbdisk-hpc
64cpu-256gbmem-30gbdisk-hpc
80cpu-320gbmem-30gbdisk-hpc
96cpu-384gbmem-30gbdisk-hpc
```

## EUMETSAT Plans

Official page: https://confluence.ecmwf.int/display/EWCLOUDKB/EUMETSAT+-+VM+plans+and+flavors

`eo1` low-memory plans with network-based local storage:

```text
eo1.xsmall
eo1.small
eo1.xmedium
eo1.medium
eo1.large
```

`eo2` general purpose plans with network-based local storage:

```text
eo2.medium
eo2.large
eo2.xlarge
eo2.2xlarge
eo2.3xlarge
eo2.4xlarge
```

`eo2a` general purpose AMD plans with network-based local storage:

```text
eo2a.medium
eo2a.large
eo2a.xlarge
eo2a.2xlarge
eo2a.3xlarge
eo2a.4xlarge
eo2a.5xlarge
```

`hm` high-memory plans with network-based local storage:

```text
hm.medium
hm.large
hm.xlarge
hm.2xlarge
hm.3xlarge
hm.4xlarge
```

`hmd` high-memory plans with local SSD storage. The official page notes that this may be a constrained resource:

```text
hmd.medium
hmd.large
hmd.xlarge
hmd.2xlarge
hmd.3xlarge
```

The official page says to ignore `hmw` plans because they are Windows-based and EWC does not offer Windows machines.

`vm.a6000` GPU plans:

```text
vm.a6000.1
vm.a6000.2
vm.a6000.4
vm.a6000.8
```

For EUMETSAT GPU plans, the official page says to use an instance type with a name ending in `-eumetsat-gpu`, for example `ubuntu-22.04-eumetsat-gpu`.

## Safe Answer Pattern

```text
Workflow type: infrastructure.

ewccli 0.10.0 does not have a command that lists every VM flavour. It accepts a selected flavour through `ewc infra create --flavour-name <flavour-name>`.

The full list is federee-specific:
- ECMWF: <official ECMWF VM plans link>
- EUMETSAT: <official EUMETSAT VM plans link>

Defaults from ewccli are:
- ECMWF (CCI1, CCI2): `4cpu-4gbmem-30gbdisk`
- EUMETSAT (WAW3-1): `eo1.large`
- EUMETSAT (ECIS-R1, ECIS-R2): `4cpu-4gbmem`

For <selected-federee>, the currently documented plan names are: ...

Validation status: this answer used the dated official KB snapshot in the skill. Recheck the official KB before treating availability or pricing as current.
```
