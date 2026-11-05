# Installation

Installing exposes the skill folders to your agent; it does not install runtime tools (`eumdac`, `ewc`, `firecube`)
or configure service credentials. Those are needed only for the workflows you run.

## One command per agent

The repository is a Claude Code / Codex plugin marketplace (`.claude-plugin/marketplace.json`) and a plain folder of
skills, so each agent installs all six skills with one command from the public repository
<https://github.com/eumetsat/skills>.

| Agent | Install | Then |
| --- | --- | --- |
| Claude Code | `/plugin marketplace add eumetsat/skills` then `/plugin install eumetsat-skills@eumetsat` | `/reload-plugins`; `/plugin` lists the six skills |
| OpenAI Codex | `codex plugin marketplace add eumetsat/skills` then `codex plugin add eumetsat-skills@eumetsat` | restart Codex; the skills appear as `eumetsat-skills:<name>` |
| OpenCode | `npx skills add eumetsat/skills -g -a opencode --skill '*' -y` | `opencode debug skill` lists them |
| Other skills-compatible agents | `npx skills add eumetsat/skills -g -a <agent> --skill '*' -y` | see <https://agentskills.io/clients> for the directory each client reads |

The [skills CLI](https://skills.sh) accepts several agents at once (`-a claude-code -a codex -a opencode`), one
skill (`--skill eumdac`), and a project-only install (drop `-g`). Updating is the same command again
(`claude plugin update eumetsat-skills@eumetsat`, `codex plugin update`, or `npx skills update`); uninstalling is
`claude plugin uninstall eumetsat-skills@eumetsat`, `codex plugin remove eumetsat-skills@eumetsat`, or
`npx skills remove`.

Behind a proxy or without GitHub access, clone the repository and use the manual sections below.

## Manual installation from a checkout

```bash
git clone https://github.com/eumetsat/skills.git eumetsat-skills
cd eumetsat-skills
```

The sections below symlink skill folders into the directory each client reads. Keep the checkout in place while its
symlinks are installed; `git pull` updates every linked skill.

### Codex and VS Code Copilot

From the repository root, expose every skill under `skills/` in the user skill directory:

```bash
mkdir -p "$HOME/.agents/skills"
for skill in $(ls skills); do
  ln -s "$PWD/skills/$skill" "$HOME/.agents/skills/$skill"
done
```

To install only some skills, replace `$(ls skills)` with the names you need, for example `eumdac ewccli`. `ln` reports an error if a destination already exists. Inspect that installation before deciding whether to replace it.

Verify the links:

```bash
for skill in $(ls skills); do
  test -f "$HOME/.agents/skills/$skill/SKILL.md" && printf '%s: installed\n' "$skill"
done
```

For a project installation, create `.agents/skills` in the consuming project and link each selected folder using its absolute checkout path. Keep the checkout in place while its symlinks are installed.

Reload your agent session and select the skill explicitly. In VS Code, check the Skills list under Chat Customizations. See the [Codex skill documentation](https://developers.openai.com/codex/skills) and [VS Code skill documentation](https://code.visualstudio.com/docs/agent-customization/agent-skills) for client-specific discovery and settings.

### Claude Code

From the repository root:

```bash
mkdir -p "$HOME/.claude/skills"
for skill in $(ls skills); do
  ln -s "$PWD/skills/$skill" "$HOME/.claude/skills/$skill"
done
```

Each skill must be exposed directly as `<skill-name>/SKILL.md`. A clone nested inside the discovery directory is not itself a skill. For a project installation, expose the selected folders under the consuming project's `.claude/skills/`. See [Claude Code skills](https://code.claude.com/docs/en/skills).

### OpenCode

From the repository root:

```bash
mkdir -p "$HOME/.config/opencode/skills"
for skill in $(ls skills); do
  ln -s "$PWD/skills/$skill" "$HOME/.config/opencode/skills/$skill"
done
```

For a project installation, use the consuming project's `.opencode/skills/`. See [OpenCode skills](https://opencode.ai/docs/skills/).

### Windows PowerShell

Copy selected folders from the repository root when symlinks are unavailable:

```powershell
$destination = Join-Path $HOME '.agents/skills'
New-Item -ItemType Directory -Force $destination | Out-Null
foreach ($skill in (Get-ChildItem -Directory 'skills').Name) {
    $target = Join-Path $destination $skill
    if (Test-Path $target) { throw "Already installed: $target" }
    Copy-Item -Recurse (Join-Path 'skills' $skill) $target
    if (-not (Test-Path (Join-Path $target 'SKILL.md'))) { throw "Missing SKILL.md: $target" }
}
```

Choose the destination appropriate to your client from the sections above. Copied folders require a fresh copy when you update this checkout.

## Service access

The ESF MCP service is internal to EUMETSAT, and installing `esf-satellite-data` does not grant
access: the MCP endpoint and credentials come only from your service administrator, with no public
request channel yet.

The Feature Database Python client (`feature-db-client`) is a public package; installing it needs no
entitlement. The Feature Database service it talks to is internal: an authorised API endpoint and API
key still come only from your service administrator, with no public request channel yet.

Follow each skill's connection instructions without sharing credentials in chat; without service
access, the skill explains this and stops.
