# EWCCLI Infrastructure Commands

Use this reference for direct `ewc infra` OpenStack server workflows.

`ewc infra` is not a general OpenStack administration interface. In `ewccli 0.10.0`, it covers server create/show/list/delete workflows only. It does not expose DNS, S3, Kubernetes, floating DNS records, or DNS zone management commands.

If the request is about images, VM plans/flavours, login/profile, Hub, custom catalogues, troubleshooting, official links, or any non-`ewccli` workflow, return to the routing tables in [SKILL.md](../SKILL.md).

## Safety Boundary

`ewc infra create` and `ewc infra delete` are state-changing OpenStack operations. Confirm profile, server name, target federee, and dry-run expectations before suggesting execution. Do not run live commands without explicit user approval and usable credentials.

## Help Checks

Run the group help before giving exact flags:

```bash
ewc infra --help
```

Some `ewc infra <command> --help` calls initialize profile/OpenStack configuration before printing help and can emit missing-credential errors when no profile or OpenStack config exists. Treat subcommand help as safe only in a configured environment, and sanitize any paths or credential-related output before sharing.

## Profile

`ewc infra` loads a profile with `--profile`; otherwise it uses the default profile.

```bash
ewc infra --profile <profile-name> list
```

`--profile` is an `ewc infra` group option. Put it before the infra subcommand:

```bash
ewc infra --profile <profile-name> list
ewc infra --profile <profile-name> show <server-name>
```

Do not suggest this form for infra commands:

```bash
ewc infra list --profile <profile-name>
```

The profile supplies federee, tenant, application credentials, and SSH key paths unless overridden.

`ewc infra` validates the loaded profile before dispatching to `list`, `show`, `create`, or `delete`. A manually edited profile can fail with missing `ssh_public_key_path` or `ssh_private_key_path` even for `list`; route those cases to [auth-profiles.md](auth-profiles.md) or [troubleshooting.md](troubleshooting.md).

For VM plan/flavour selection, use [vm-plans.md](vm-plans.md). `ewccli 0.10.0` accepts `--flavour-name`, but it does not expose a dedicated `ewc` command to list all available flavours.

## List And Show

List servers created by EWC CLI:

```bash
ewc infra --profile <profile-name> list
```

The list shows `Name`, `Status`, `Networks`, `Keypair`, and `Flavor` columns.

List all visible servers, including machines not created by EWC CLI:

```bash
ewc infra --profile <profile-name> list --show-all
```

Show one server:

```bash
ewc infra --profile <profile-name> show <server-name>
```

`show` also reports the root volume size in GB and any extra volumes with their mount points. When a server was booted from a volume, the image row may read `N/A (booted from volume)`.

## Create

Dry-run first:

```bash
ewc infra --profile <profile-name> create <server-name> --dry-run
```

Real create template:

```bash
ewc infra --profile <profile-name> create <server-name> \
  --image-name <ewc-virtual-image-name-or-supported-ewccli-selector> \
  --flavour-name <flavour-name> \
  --networks <network-name> \
  --security-groups <security-group-name>
```

Common optional flags include:

```text
--dry-run
--force
--keypair-name / -kp
--image-name / -ig
--flavour-name / -fr
--external-ip
--networks / -n
--security-groups / -sg
--root-volume
--extra-volume
--ssh-public-key-path
--ssh-private-key-path
--auth-url / -url
--application-credential-id
--application-credential-secret
```

Since `0.10.0`, every server boots from a volume in all regions. `--root-volume <GB>` sets the root volume size (default `50`); it applies wherever boot from volume is used, which is now always. `--extra-volume <GB>` attaches an additional data volume and can be repeated for several volumes. When redeploying over an existing server, `--networks` and `--security-groups` may be given in any order; they are compared as sets.

Do not recommend passing secrets on the command line unless the user explicitly needs non-interactive execution; profiles, `clouds.yaml`, `openrc`, or secret-managed environment variables reduce shell-history exposure.

If a public IP is needed for direct SSH access, include:

```bash
--external-ip
```

## Delete

Dry-run first:

```bash
ewc infra --profile <profile-name> delete <server-name> --dry-run
```

Real delete:

```bash
ewc infra --profile <profile-name> delete <server-name>
```

Use `--force` only when the user explicitly wants to delete a machine that may not have been created by `ewccli`.

Before deletion, `ewc infra delete` detaches and releases the server's external/floating IP and removes ewccli-tagged extra volumes, then prints the backend's delete message. VMs in `ERROR` state without network addresses are handled gracefully.

## Defaults From Source

The inspected `ewccli 0.10.0` source includes these defaults:

| Setting | ECMWF (CCI1/CCI2) | EUMETSAT (WAW3-1) | EUMETSAT (ECIS-R1/ECIS-R2) |
| --- | --- | --- | --- |
| Auth URL | `https://auth.os-api.cci1.ecmwf.int:443` (CCI2 uses `...cci2...`) | `https://keystone.cloudferro.com:5000` | `https://keystone.api.r1.cloud.eumetsat.int` (R2 uses `...r2...`) |
| Default CPU image selector | `Rocky-9` | `Rocky-9` | `Rocky-9` |
| Default CPU flavour | `4cpu-4gbmem-30gbdisk` | `eo1.large` | `4cpu-4gbmem` |
| Default network | `private` | `private` | `private` |
| Default external network | `external-internet` | `external` | `external` |
| Default security group | `ssh` | `ssh` | `ssh` |
| Default root volume | 50 GB (boot from volume, all regions) | 50 GB | 50 GB |

Regions are selected at login time with `ewc login --region` (`CCI1`, `CCI2`, `WAW3-1`, `ECIS-R1`, `ECIS-R2`), validated against the federee. Since `0.10.0`, boot from volume is unconditional in every region (previously only ECIS-R1/ECIS-R2), with a default root volume of 50 GB sized by `--root-volume`.

Treat these as version-specific defaults. `Rocky-9` is an `ewccli` short selector/default, not the dated official image name in the EWC Virtual Images table. For exact official image names, use [vm-images.md](vm-images.md) and copy from the `EWC Virtual Image name` column.

For the complete federee-specific VM plan/flavour lists, use [vm-plans.md](vm-plans.md). Do not infer generic small/medium/large categories beyond the exact names documented there.
