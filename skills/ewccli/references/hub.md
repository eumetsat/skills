# EWC Community Hub

Use this reference for `ewc hub` item discovery and deployment workflows.

## Safety Boundary

`ewc hub list` and `ewc hub show` are discovery commands, but they can download or refresh the Hub catalogue under `$HOME/.ewccli/items.yaml`.

Do not use `ewc hub list` as proof that `ewc login` or OpenStack authentication works. Hub catalogue listing can work without an authenticated EWC/OpenStack profile.

`ewc hub deploy` can create cloud resources, clone item sources under `$HOME/.ewccli/outputs`, run Ansible, create OpenStack servers, attach networking, and use SSH keys. Confirm cost/resource implications and prefer `--dry-run` for first passes.

## Help Checks

Run before giving exact flags:

```bash
ewc hub --help
ewc hub list --help
ewc hub show --help
ewc hub deploy --help
```

## Catalogue Selection

By default, `ewccli` uses the official EWC Community Hub catalogue downloaded to:

```text
$HOME/.ewccli/items.yaml
```

Use a custom catalogue file with:

```bash
ewc hub --path-to-catalog <path-to-catalog.yaml> list
ewc hub --path-to-catalog <path-to-catalog.yaml> show <item>
ewc hub --path-to-catalog <path-to-catalog.yaml> deploy <item>
```

`--path-to-catalog` can also be set with `EWC_CLI_PATH_TO_CATALOGUE`.

## List And Show

List available items:

```bash
ewc hub list
```

Force catalogue re-download:

```bash
ewc hub list --force
```

Show item details:

```bash
ewc hub show <item>
```

Use `ewc hub list` first and copy the exact item name from the Item column.

## Deploy

Basic deployment template:

```bash
ewc hub deploy <item> \
  --profile <profile-name> \
  --server-name <server-name>
```

Dry-run template:

```bash
ewc hub deploy <item> \
  --profile <profile-name> \
  --server-name <server-name> \
  --dry-run
```

Common optional deployment flags include:

```text
--profile
--server-name
--item-inputs / -iu key=value
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

Since `0.10.0`, every deployed server boots from a volume in all regions. `--root-volume <GB>` sets the root volume size (default `50`), and `--extra-volume <GB>` attaches additional data volumes (repeatable). `--networks` and `--security-groups` may be listed in any order when redeploying; they are compared as sets.

Do not recommend passing secrets on the command line unless the user explicitly needs non-interactive execution; environment variables or profiles reduce shell-history exposure.

## Item Inputs

Items may define required and default inputs. Pass user inputs as key-value pairs:

```bash
ewc hub deploy <item> \
  --profile <profile-name> \
  --item-inputs mymandatoryinput=value \
  --item-inputs retries=3
```

Values are parsed with YAML syntax, so lists/dictionaries need shell-safe quoting:

```bash
ewc hub deploy <item> --item-inputs 'names=["a", "b"]'
```

If required inputs are missing, `ewccli` reports the missing keys. Use `ewc hub show <item>` to inspect expected inputs before retrying.

## Resource Confirmation Checklist

Before a real deployment, confirm:

- Target federee: `EUMETSAT` or `ECMWF`.
- Profile name and tenant.
- Item name and item version if shown.
- Server name.
- Whether an external IP is requested.
- Image, flavour, networks, and security groups if overriding defaults.
- SSH key paths and whether the user can access the private key.
- Whether `--force` may recreate or overwrite local deployment outputs.
