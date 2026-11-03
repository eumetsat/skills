# EWCCLI Troubleshooting

Use this reference for diagnosing `ewccli` failures. Always ask for the exact command and sanitized output.

## First Checks

Run credential-free checks:

```bash
ewc version
ewc --help
ewc login --help
ewc hub --help
ewc infra --help
python -c "import ewccli; print(ewccli.__file__)"
```

Avoid using `ewc infra create --help` or `ewc infra delete --help` as generic credential-free checks. In `ewccli 0.10.0`, infra subcommand help can initialize profile/OpenStack configuration and print missing-credential diagnostics before showing help.

If `ewc` is missing:

```bash
python -m pip show ewccli
python -m pip install 'ewccli==0.10.0'
```

If the installed script is outside `PATH`, add the script directory to the user's shell startup file.

## Version Drift

The current skill is grounded in `ewccli 0.10.0`. If behavior differs, inspect local help and package metadata:

```bash
ewc version
ewc --help
python -m pip show ewccli
```

Prefer installed help over this skill for exact flags.

## Profile Not Found

Profiles live in:

```text
$HOME/.ewccli/profiles
```

List profile section names without printing secrets using the [Safe Profile-Name Inspection](auth-profiles.md#safe-profile-name-inspection) script in auth-profiles.md.

If the wrong profile is used, pass it explicitly:

```bash
ewc hub deploy <item> --profile <profile-name> --dry-run
ewc infra --profile <profile-name> list
```

For `ewc infra`, `--profile` belongs to the `infra` group. Put it before the subcommand:

```bash
ewc infra --profile <profile-name> list
```

Do not use:

```bash
ewc infra list --profile <profile-name>
```

If `ewc infra list --profile <profile-name>` still reports that the default profile does not exist, correct the option placement before diagnosing credentials.

## Command Typos

If the user runs a misspelled command such as:

```bash
ewc infa
```

explain that `infa` is not a registered command and point them to:

```bash
ewc --help
ewc infra --help
```

Do not treat a command typo as an unsupported EWC service request.

## Incomplete Manual Profiles

If an infra command fails with a missing profile key, for example:

```text
`ssh_public_key_path` key is missing from your profile <profile-name>, please rerun ewc login.
```

explain that `ewccli 0.10.0` validates the full profile before running infra subcommands. This can affect `ewc infra list` as well as create/delete workflows.

Recovery guidance:

1. Prefer creating a new complete profile with `ewc login --profile <new-profile-name>`.
2. If the user wants to keep the same profile name, back up the profile file and remove or rename the incomplete section only after explicit confirmation, then run `ewc login --profile <profile-name>`.
3. If the profile was manually edited, verify required keys exist without printing values.
4. Check that the referenced SSH public/private key files exist and match.

Check required keys without printing secrets using the [Safe Profile Schema Check](auth-profiles.md#safe-profile-schema-check) script in auth-profiles.md.

## Existing Profile During Login

`ewc login` does not abort just because `$HOME/.ewccli/profiles` exists; it checks the resolved target section instead. See [Existing Profiles](auth-profiles.md#existing-profiles) in auth-profiles.md for how the target section is resolved and the recovery options.

## Credential Errors

Use the official European Weather Cloud website, `https://www.europeanweather.cloud/`, when directing users to EWC.

For requesting OpenStack application credentials, see [Request OpenStack Application Credentials](auth-profiles.md#request-openstack-application-credentials) in auth-profiles.md.

Check credential source order:

1. Environment variables such as `OS_APPLICATION_CREDENTIAL_ID`, `OS_APPLICATION_CREDENTIAL_SECRET`, and `OS_AUTH_URL`.
2. `ewccli` profile config.
3. OpenStack config such as `OS_CLIENT_CONFIG_FILE` or `$HOME/.config/openstack/clouds.yaml`.

Do not ask users to paste secrets. Ask them to confirm whether a value is set or to run commands that redact values.

## Tenant Name Questions

Give only the convention `<memberstate>-<organization>-<projectname>` and the EWC Support fallback. Do not invent or suggest example tenant names, and do not ask the user to paste `openrc`, `clouds.yaml`, profiles, or credential values. Full guidance: [auth-profiles.md](auth-profiles.md#tenant-name-convention-and-sources).

## SSH Key Errors

`ewccli` verifies that SSH public/private key files both exist and match. If one side is missing, provide the key paths and fix the pair before deployment.

Safe checks:

```bash
test -f "$HOME/.ssh/id_rsa" && echo "private key exists"
test -f "$HOME/.ssh/id_rsa.pub" && echo "public key exists"
derived_pub=$(mktemp)
ssh-keygen -y -f "$HOME/.ssh/id_rsa" > "$derived_pub"
diff "$derived_pub" "$HOME/.ssh/id_rsa.pub"
rm -f "$derived_pub"
```

Do not print private key contents.

## Hub Catalogue Errors

If `ewc hub list` or `show` fails:

- Check network access to the official catalogue URL.
- Force refresh with `ewc hub list --force`.
- Confirm `$HOME/.ewccli/items.yaml` exists and is valid YAML.
- For custom catalogues, confirm the path is a file and contains `spec.items`.

## Deployment Failures

Collect:

- Exact command, with secrets removed.
- `ewc version`.
- Profile name, federee, and tenant name.
- Item or server name.
- Whether `--dry-run` was used.
- Sanitized OpenStack or Ansible error.

Common causes:

- Missing required `--item-inputs`.
- Item is not deployable.
- Wrong federee/profile.
- Invalid image, flavour, network, or security group.
- Private or unreachable item source repository.
- Existing output directory when `--force` is not used.
- SSH key mismatch or missing key file.

## Debug Logging

The source reads `EWC_CLI_DEBUG_LEVEL`, defaulting to `INFO`. Use a more verbose level only for sanitized reproduction:

```bash
EWC_CLI_DEBUG_LEVEL=DEBUG ewc hub show <item>
```

Review output before sharing; debug logs can include paths and environment-derived context.
