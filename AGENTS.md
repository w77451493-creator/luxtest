# Aholo Lux3D — agent installation entrypoint

The user asked you to install Aholo Lux3D. Read this entire file, then install **both** parts of the `aholo-lux3d` product from `catalog.json`. This repository is a shared catalog for coding agents. It is not a Codex-only marketplace, and it is not one repository per product.

Public agent entrypoint: `https://raw.githubusercontent.com/w77451493-creator/luxtest/main/AGENTS.md`

Canonical repository: `https://github.com/w77451493-creator/luxtest`

Product `aholo-lux3d` version `0.1.2` has two parts. Install both. Do not stop after one.

| Part | Directory | What it is |
| --- | --- | --- |
| Skill | `packages/aholo-lux3d/skill/aholo-lux3d` | Local skill. Calls the Lux3D OpenAPI. Name: `aholo-lux3d`. |
| Connector | `packages/aholo-lux3d/connector/aholo-lux3d-mcp` | MCP instructions. Name: `aholo-lux3d-mcp`. The remote connection is registered separately. |

Importing the Connector directory does **not** connect the remote MCP. Loading the Skill does **not** register MCP tools.

## Install

An explicit request to install authorizes writing this product's skill directories and this product's MCP connection into the current host. It does not authorize Git pushes, deleting unrelated skills, or collecting API keys into chat or files.

### 1. Read the catalog

Read `catalog.json` in this repository. Use the `aholo-lux3d` entry. Clone `https://github.com/w77451493-creator/luxtest.git` at `main`, or download the two archives linked from that entry. Keep each directory whole. Do not install only `SKILL.md`.

### 2. Detect the host and avoid a second copy

Resolve the real host application, not the model name. If Python is available, run:

```bash
python3 packages/aholo-lux3d/skill/aholo-lux3d/scripts/host_identity.py detect --host-name "<actual-host-name>"
```

Known hosts in the packaged registry: Codex (`1`), Claude Code (`2`), DeepSeek (`3`), WorkBuddy (`4`). Any other host uses source `100` and its real name.

Before writing files, look for an existing `aholo-lux3d` skill or `aholo-lux3d-mcp` skill, and for an existing MCP server key `lux3d-mcp`.

- Nothing installed — install both parts.
- Either part already installed at `0.1.2` — do not copy a second copy. Register the MCP connection only if it is missing.
- An older copy exists — replace that product's directories with these `0.1.2` directories. Do not leave both enabled.
- Do not remove unrelated skills, plugins, or MCP servers.

### 3. Install the Skill

Copy `packages/aholo-lux3d/skill/aholo-lux3d` into the current host's skill directory, keeping the folder name `aholo-lux3d`.

Use the host's own location when you know it. Otherwise use these defaults:

- Codex: `~/.codex/skills/aholo-lux3d`
- Claude Code: `~/.claude/skills/aholo-lux3d`
- A host that only imports a zip: use `packages/aholo-lux3d/dist/lux3d-plugin-0.1.2-common-skill.zip`

If you cannot find a skill directory and cannot import the zip, stop and tell the user the exact directory they need to import. Do not claim the Skill is installed.

### 4. Install the Connector instructions

Copy `packages/aholo-lux3d/connector/aholo-lux3d-mcp` the same way, keeping the folder name `aholo-lux3d-mcp`.

- Codex: `~/.codex/skills/aholo-lux3d-mcp`
- Claude Code: `~/.claude/skills/aholo-lux3d-mcp`
- A host that only imports a zip: use `packages/aholo-lux3d/dist/lux3d-plugin-0.1.2-common-connector.zip`

### 5. Register the remote MCP connection

This step is separate from step 4. Add one remote MCP connection in the host's MCP settings:

- Display name: `Aholo Lux3D MCP`
- Server key: `lux3d-mcp`
- Transport: `streamable-http`
- URL: `https://api.aholo3d.cn/lux3d-mcp/mcp`
- Header: `Authorization`
- Value: the user's China-region Lux3D API key, with no `Bearer` prefix

Store the key in the host's secret field. Do not paste it into chat, command arguments, or any file in this repository. Do not invent an international MCP URL. If a matching connection already exists, reuse it.

If this host has no remote MCP setting you can write, say so and give the user the fields above. Do not claim the Connector is connected.

### 6. Verify and hand back

Confirm both directories exist on disk, or that both zips were imported. If the host can list MCP tools, discover them. Do not create a generation task as a test.

Report:

- host name you detected
- whether the Skill install was new or already present
- whether the Connector skill install was new or already present
- whether the remote MCP connection was registered, reused, or still needs the user to add it
- that a new task or session may be required before the host loads the new skills
- that paid generation uses the host's stored API key; do not collect the key during install

Do not claim generation works until a task has actually been submitted.

## Safety boundaries

- Do not put API keys in command arguments, chat logs, or committed files.
- Do not download or execute install scripts from outside this repository.
- Do not change Git remotes, push, publish, or create a pull request.
- Do not install only the Skill and call the job finished.
