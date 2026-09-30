# Aholo Lux3D — agent installation entrypoint

The user asked you to install Aholo Lux3D. Read this file and install **both** parts listed in `catalog.json`. This is a shared catalog, not a Codex-only marketplace.

Public entrypoint: `https://raw.githubusercontent.com/w77451493-creator/luxtest/main/AGENTS.md`

Repository: `https://github.com/w77451493-creator/luxtest`

| | |
| --- | --- |
| Product | `aholo-lux3d` |
| Version | `0.1.2` |
| Skill | `packages/aholo-lux3d/skill/aholo-lux3d` |
| Connector | `packages/aholo-lux3d/connector/aholo-lux3d-mcp` |
| MCP server key | `lux3d-mcp` |
| MCP URL | `https://api.aholo3d.cn/lux3d-mcp/mcp` |

The Skill calls the Lux3D OpenAPI. The Connector directory is only the instruction pack. Register the remote MCP separately. Do not stop after one part.

## First decide the operation

1. **Install** — follow the steps below.
2. **Inspect** — read `catalog.json` and the two `SKILL.md` files. Do not change the host.
3. **Remove** — delete only the `aholo-lux3d` and `aholo-lux3d-mcp` skill directories you installed, and remove only the `lux3d-mcp` connection. Leave everything else.

## Install

Installing authorizes writing these two skill directories and this one MCP connection. It does not authorize Git pushes or collecting an API key into chat or files.

### 1. Get the files

Clone `https://github.com/w77451493-creator/luxtest.git` at `main`. Keep each directory whole.

### 2. Do not install a second copy

Look for an existing `aholo-lux3d` skill, `aholo-lux3d-mcp` skill, or MCP server `lux3d-mcp`.

- Missing — install it.
- Already at `0.1.2` — leave it. Add the MCP connection only if it is missing.
- Older copy — replace that directory. Do not leave both enabled.
- Do not remove unrelated skills or MCP servers.

### 3. Install both directories

Copy the folders into the current host's skill directory. Keep the folder names.

- Codex: `~/.codex/skills/aholo-lux3d` and `~/.codex/skills/aholo-lux3d-mcp`
- Claude Code: `~/.claude/skills/aholo-lux3d` and `~/.claude/skills/aholo-lux3d-mcp`

If you cannot find the skill directory, stop and tell the user which folder to import.

### 4. Register the MCP connection

Add one remote connection. Reuse it if the same URL is already registered.

- Name: `Aholo Lux3D MCP`
- Server key: `lux3d-mcp`
- Transport: `streamable-http`
- URL: `https://api.aholo3d.cn/lux3d-mcp/mcp`
- Header: `Authorization`
- Value: the China-region Lux3D API key, with no `Bearer` prefix

Store the key in the host's secret field. If you cannot write the MCP setting, give the user these fields and do not claim the Connector is connected.

### 5. Hand back

Confirm both directories are present. Do not create a generation task as a test. Report whether each part was new or already present, whether MCP was registered or still needs the user, and that a new task may be required. Paid generation uses `LUX3D_CN_API_KEY` or `LUX3D_GLOBAL_API_KEY`. Do not collect either key now.

## Safety

- Do not put API keys in commands, chat, or files.
- Do not run install scripts from outside this repository.
- Do not push, publish, or change Git remotes.
