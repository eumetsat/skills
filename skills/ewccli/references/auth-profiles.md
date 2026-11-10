# EWCCLI Login And Profiles

Use this reference for `ewc login`, profile files, OpenStack application credentials, federee selection, and SSH key safety.

## Credential Safety

Never print or commit:

- OpenStack application credential IDs or secrets.
- Private SSH keys or base64-encoded SSH keys.
- `$HOME/.ewccli/profiles`.
- OpenStack `clouds.yaml` files or environment dumps containing `OS_*` secrets.

Use placeholders:

```text
<application-credential-id>
<application-credential-secret>
<tenant-name>
<profile-name>
```

## Official EWC Links

Use the official European Weather Cloud website:

```text
https://www.europeanweather.cloud/
```

For OpenStack application credential requests, use the official EWC Knowledge Base article:

```text
https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+OpenStack+API+access+-+How+to+request+Openstack+Application+Credentials
```

## Request OpenStack Application Credentials

When users need OpenStack application credentials, direct them to the official EWC Knowledge Base process: raise a ticket in the EWC Support Portal.

```text
https://support.europeanweather.cloud/
```

Tell the user to include:

- Ticket title: `Openstack App Credentials Request`.
- Tenant name in the form `<memberstate>-<organization>-<projectname>`.
- Scope and description of use.
- Owner, if different from the requestor.
- Any other relevant note.

If the requestor is not the tenancy administrator, include the tenancy administrator as a participant in the request.

The provided credential files can include:

- `openrc`, which can be sourced to export OpenStack environment variables.
- `clouds.yaml`, which can be installed under `$HOME/.config/openstack/clouds.yaml`.

Either file can be used as an alternative to the other. If the user receives a `clouds.yaml`, prefer configuring OpenStack securely and running `ewc login` without pasting secrets into chat.

## Credential Source To EWCCLI Profile Flow

Use this route when the user asks how to authenticate, log in, prepare credentials, or use received `openrc` / `clouds.yaml` files.

Keep these steps separate:

1. Request OpenStack application credentials through the official EWC KB/support process.
2. EWC provides credential material, typically `openrc` and/or `clouds.yaml`.
3. The user installs/configures exactly one credential source:
   - install the received `clouds.yaml` under `$HOME/.config/openstack/clouds.yaml`, or
   - source the received `openrc`, or
   - use secret-managed environment variables, or
   - let `ewc login` prompt for application credential values with hidden input.
4. Run `ewc login` to create the `ewccli` profile.
5. `ewc login` writes the `ewccli` profile under `$HOME/.ewccli/profiles`.

Do not say or imply that `ewc login` creates, installs, writes, or configures `clouds.yaml` or `openrc`. It reads existing OpenStack credential sources; it writes the `ewccli` profile.

Do not use `ewc hub list` as proof that login or OpenStack authentication works. `ewc hub list` is catalogue discovery and can work without an authenticated EWC/OpenStack profile.

Safe response shape:

```text
First request OpenStack application credentials using the official EWC KB process:
https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+OpenStack+API+access+-+How+to+request+Openstack+Application+Credentials

EWC provides credential files such as `openrc` and/or `clouds.yaml`. Configure one of those locally, or let `ewc login` prompt for application credential values. Then run `ewc login` to create the ewccli profile. `ewc login` consumes existing credential sources; it does not create or configure `openrc` or `clouds.yaml`.
```

## Tenant Name Convention And Sources

For tenant-name questions, explain the EWC tenant naming convention and direct the user to EWC Support if they do not remember the tenant name. Do not invent a concrete tenant name, do not provide plausible examples, and do not ask the user to paste full `openrc`, `clouds.yaml`, profile files, environment dumps, application credential IDs, or secrets.

Tenant names use the pattern `<memberstate>-<organization>-<projectname>`, where:

- `memberstate` is the member state identifier, such as `de`, `int`, or `it`.
- `organization` is the organization identifier.
- `projectname` is the project identifier.

The user can learn or confirm the tenant name by:

- Asking EWC Support.
- Using the naming convention to recognize or remember the assigned value.

Do not present `openrc`, `clouds.yaml`, OpenStack project fields, current shell variables, or existing `ewccli` profiles as authoritative tenant-name sources. Those are OpenStack or local configuration concepts and may be unavailable when the user is trying to create the `ewccli` profile.

## Profile Location

`ewccli` stores profiles in:

```text
$HOME/.ewccli/profiles
```

Default generated SSH keys are stored under:

```text
$HOME/.ewccli/.ssh/
```

The profile format documented upstream is:

```ini
[my-profile]
federee = EUMETSAT or ECMWF
tenant_name = <memberstate>-<organization>-<projectname>
application_credential_id =
application_credential_secret =
ssh_public_key_path =
ssh_private_key_path =
```

Manual profile edits are fragile. `ewccli 0.10.0` loads and validates the full profile before running infra subcommands, including read-style commands such as `ewc infra list`. A hand-edited profile that omits `ssh_public_key_path` or `ssh_private_key_path` can fail before the OpenStack request is made.

If a user has hand-edited `$HOME/.ewccli/profiles`, prefer one of these recovery paths:

1. Create a new complete profile with `ewc login --profile <new-profile-name>` and switch commands to that profile.
2. If the user wants to keep the same name, back up the profile file and remove or rename the incomplete section only after explicit confirmation, then run `ewc login --profile <profile-name>`.
3. If editing manually is unavoidable, verify required keys exist without printing secret values.

### Safe Profile Schema Check

```bash
python - <<'PY'
from configparser import ConfigParser
from pathlib import Path

profile_name = "<profile-name>"
required = [
    "federee",
    "ssh_public_key_path",
    "ssh_private_key_path",
]
optional = [
    "tenant_name",
    "application_credential_id",
    "application_credential_secret",
]

profiles = Path.home() / ".ewccli" / "profiles"
cfg = ConfigParser()
cfg.read(profiles)

if profile_name not in cfg:
    print(f"missing profile: {profile_name}")
    raise SystemExit(1)

missing = [key for key in required if not cfg[profile_name].get(key)]
if missing:
    print("missing keys: " + ", ".join(missing))
    raise SystemExit(1)

optional_missing = [key for key in optional if not cfg[profile_name].get(key)]
if optional_missing:
    print("optional keys not set in profile: " + ", ".join(optional_missing))

print("profile has required keys")
PY
```

Do not print the value of `application_credential_id`, `application_credential_secret`, SSH key contents, or the whole profile file.

## Configuration Precedence

The upstream README describes this order:

1. Environment variables.
2. CLI config.
3. Other config, such as OpenStack `clouds.yaml` or Kubernetes `kubeconfig`.

The login code also checks OpenStack config from `OS_CLIENT_CONFIG_FILE`, `$HOME/.config/openstack/clouds.yaml`, or `/etc/openstack/clouds.yaml`, and may skip OpenStack credential prompts when a usable config exists.

## Login Command

Interactive path:

```bash
ewc login
```

Preferred non-secret command shape. Configure a protected `clouds.yaml`, source `openrc`, or set secret-managed environment variables before running `ewc login`; otherwise let `ewc login` prompt for application credential values with hidden input:

```bash
ewc login \
  --profile <profile-name> \
  --federee EUMETSAT \
  --region CCI1 \
  --tenant-name <tenant-name> \
  --ssh-public-key-path $HOME/.ssh/id_rsa.pub \
  --ssh-private-key-path $HOME/.ssh/id_rsa
```

For non-interactive automation, prefer a protected `clouds.yaml`, a sourced `openrc`, or environment variables managed by the user's secret store before invoking `ewc login`. Avoid putting `--application-credential-secret` directly in shell history.

`--federee` accepts `EUMETSAT` or `ECMWF`. `--region` (env `EWC_CLI_LOGIN_REGION`) accepts `CCI1`, `CCI2`, `WAW3-1`, `ECIS-R1`, or `ECIS-R2`, validated against the federee: `ECMWF` allows `CCI1`/`CCI2`; `EUMETSAT` allows `WAW3-1`/`ECIS-R1`/`ECIS-R2`. If omitted, `ewc login` prompts interactively. For the tenant name pattern and sourcing rules, see [Tenant Name Convention And Sources](#tenant-name-convention-and-sources) above. Do not invent a concrete tenant name; use `<memberstate>-<organization>-<projectname>` unless the user provides the real tenant.

## After Login Validation

Separate local profile validation from live OpenStack validation:

- Local check: confirm `ewc login` completed and created an `ewccli` profile under `$HOME/.ewccli/profiles` without printing the profile file.
- Catalogue check: `ewc hub list` only proves the Community Hub catalogue can be listed; it does not prove login or OpenStack authentication.
- Live credential check: a read-only infra command such as `ewc infra --profile <profile-name> list` exercises the configured profile and OpenStack credentials, but it requires live EWC/OpenStack access and may fail for service-side or permission reasons.

This is a read-only command; it may run without extra confirmation once a working profile exists, per [SKILL.md](../SKILL.md) rule 2. Never run `ewc login` to create or fix a profile just to make this check work. State clearly that it is a live OpenStack call:

```bash
ewc infra --profile <profile-name> list
```

## Existing Profiles

`ewc login` checks profile sections, not just whether `$HOME/.ewccli/profiles` exists. A profiles file can exist and `ewc login` can still prompt normally when the target section is missing.

The target section is resolved as:

- `--profile <profile-name>` when explicitly provided.
- Otherwise, an auto-generated name from the selected federee and tenant, such as `<federee>-<tenant-name>`.

`ewc login` may prompt for `Tenant name:` and federee before it can know the auto-generated target section. Seeing the prompt does not mean the profile file is ignored.

The command refuses to save only when the resolved target section already exists. If the user asks to replace a profile:

1. Inspect the profile names without printing secret values.
2. Ask for explicit confirmation before editing or deleting profile entries.
3. Prefer creating a new named profile when possible.

### Safe Profile-Name Inspection

```bash
python - <<'PY'
from configparser import ConfigParser
from pathlib import Path
profiles = Path.home() / ".ewccli" / "profiles"
cfg = ConfigParser()
cfg.read(profiles)
for name in cfg.sections():
    print(name)
PY
```

## SSH Keys

If SSH key paths are omitted, `ewc login` uses profile-specific defaults under `$HOME/.ewccli/.ssh`. It checks whether private and public keys exist and match. If neither exists, the command may prompt to generate a key pair.

Do not overwrite keys manually. When users provide custom key paths, verify both files exist and form a pair before deployment.
