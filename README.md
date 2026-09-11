# Aholo Lux3D — Codex plugin marketplace

A Git-hosted Codex plugin marketplace for [Aholo Lux3D](https://labs.aholo3d.com).
Users install straight from this repository. **No zip, no manual download.**

| Field | Value |
| --- | --- |
| Marketplace | `luxtest` |
| Plugin | `aholo-lux3d` |
| Selector | `aholo-lux3d@luxtest` |
| Version | `0.1.0` |
| Branch | `main` |

## Install (one line)

Paste this into any Codex task:

```
/goal Read https://raw.githubusercontent.com/w77451493-creator/luxtest/main/AGENTS.md to install Aholo Lux3D for Codex and set up a new task for me.
```

中文版：

```
/goal 读 https://raw.githubusercontent.com/w77451493-creator/luxtest/main/AGENTS.md 帮我安装 Aholo Lux3D 插件，并新建一个任务。
```

Then open a **new** Codex task and invoke the plugin with `$lux3d` or `@aholo-lux3d`.
Plugin capabilities load at task start, so a fresh task is required.

## Install (direct CLI)

```bash
codex plugin marketplace add w77451493-creator/luxtest --ref main
codex plugin add aholo-lux3d@luxtest
```

Verify:

```bash
codex plugin marketplace list
codex plugin list
```

Uninstall:

```bash
codex plugin remove aholo-lux3d@luxtest
codex plugin marketplace remove luxtest
```

## Requirements

| Item | Requirement |
| --- | --- |
| Codex | Codex CLI `0.121.0`+ (plugin marketplace support), or the current Codex / ChatGPT desktop app |
| Python | Python 3.9+ available as `python3` (`python` / `py` on Windows) |
| Network | Access to GitHub (to fetch this marketplace) and to the Lux3D API |
| API key | `LUX3D_CN_API_KEY` for the `cn` region, or `LUX3D_GLOBAL_API_KEY` for `international` |

No MCP server is required and nothing has to be downloaded by hand. The plugin ships its
own Skill and a self-contained runtime; on first use the agent runs
`python3 <installed-skill>/scripts/setup_runtime.py`, which creates a private environment
and installs the bundled dependency (`requests`). Setup does not call Lux3D and does not
need an API key.

## Layout

```
.agents/plugins/marketplace.json   Codex marketplace catalog
plugins/codex/aholo-lux3d/         Installable plugin payload (md, py, js, json + assets)
AGENTS.md                          Canonical agent install guide
```

`plugins/codex/aholo-lux3d/` is a verbatim copy of the shipped Lux3D Codex release
package: `.codex-plugin/plugin.json` manifest, `skills/lux3d/` Skill with references,
scripts, contracts and viewer runtime, plus `adapter.json` and `build-info.json`.

Do not hand-edit files inside the plugin directory. Replace the whole directory with a
new build, bump `version` in `.codex-plugin/plugin.json`, and commit.

## Troubleshooting

**Plugin does not appear after install.**
Run `codex plugin list`. Installed plugins stay invisible to the model until a task
starts, so close the current task and open a new one first. If the marketplace itself is
missing, re-run `codex plugin marketplace add w77451493-creator/luxtest --ref main`,
then `codex plugin marketplace upgrade`.

**`git ls-remote` returns 404 for other users.**
This repository must stay **public**. `codex plugin marketplace add` clones over GitHub;
a private repository 404s for everyone else.

**`CLI_DEPENDENCY_MISSING` when the plugin runs Python.**
Re-run `python3 <installed-skill>/scripts/setup_runtime.py` and retry with the
interpreter path it returns. A Python import failure does not mean the API key is invalid.

**Restricted network / internal mirror.**
`add` accepts any Git URL, so an internal mirror works:

```bash
codex plugin marketplace add https://<your-mirror>/<path>/luxtest.git --ref main
```

## Links

- Product site: https://labs.aholo3d.com
- Plugin manifest: [plugins/codex/aholo-lux3d/.codex-plugin/plugin.json](plugins/codex/aholo-lux3d/.codex-plugin/plugin.json)
- Skill entry point: [plugins/codex/aholo-lux3d/skills/lux3d/SKILL.md](plugins/codex/aholo-lux3d/skills/lux3d/SKILL.md)
