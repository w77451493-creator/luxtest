# Aholo Lux3D — Codex Plugin Marketplace

This repository is a **Codex plugin marketplace source**. It exists so you never have to
download and install an archive by hand: add this repo as a marketplace once, and the
**Aholo Lux3D** plugin is installed for you.

- Plugin: `aholo-lux3d` (Aholo Lux3D, v0.1.0)
- Marketplace name: `aholo-lux3d`
- Manifest: `.agents/plugins/marketplace.json`
- Plugin root: `plugins/aholo-lux3d/`

---

## Option A — One-line install (recommended)

Paste this into any Codex / ChatGPT desktop task:

```
/goal Read https://raw.githubusercontent.com/w77451493-creator/luxtest/main/README.md and install the Aholo Lux3D plugin for Codex, then set up a new task for me.
```

### 中文（一句话安装）

把下面这句粘进 Codex 的任意任务里：

```
/goal 读 https://raw.githubusercontent.com/w77451493-creator/luxtest/main/README.md 安装 Aholo Lux3D 插件，然后新建一个任务。
```

The agent will add the marketplace, confirm the plugin is installed, and open a fresh task.
Plugin capabilities only load at task start, so **always continue in a new task**.

---

## Option B — Manual install

```bash
# 1. Add this repository as a marketplace (GitHub shorthand, Git URL or SSH URL all work)
codex plugin marketplace add w77451493-creator/luxtest

# 2. Refresh registered marketplaces
codex plugin marketplace upgrade

# 3. Verify the source is registered
codex plugin marketplace list
```

Then restart the Codex / ChatGPT desktop app, open **Plugins**, and pick the
**Aholo Lux3D** tab. `aholo-lux3d` is marked `INSTALLED_BY_DEFAULT`, so if it is not
enabled yet, install it with one click. Start a **new task** afterwards.

To remove it later:

```bash
codex plugin marketplace remove aholo-lux3d
```

---

## Requirements

| Item | Requirement |
| --- | --- |
| Codex | Codex CLI `0.121.0`+ (plugin marketplace support), or the current Codex / ChatGPT desktop app |
| Python | Python 3.9+ available as `python3` (`python` / `py` on Windows) |
| Network | Access to GitHub (to fetch this marketplace) and to the Lux3D API |
| API key | `LUX3D_CN_API_KEY` for the `cn` region, or `LUX3D_GLOBAL_API_KEY` for `international` |

No MCP server is required. The plugin ships its own Skill and self-contained runtime;
on first use the agent runs `python3 <installed-skill>/scripts/setup_runtime.py`, which
creates a private environment and installs the bundled dependencies (`requests`).
Setup does not call Lux3D and does not need an API key.

Set the API key in your secure environment configuration — never in command arguments
or in quote files:

```bash
export LUX3D_CN_API_KEY="<your-key>"        # cn region
export LUX3D_GLOBAL_API_KEY="<your-key>"    # international region
```

---

## Use it

In the new task, mention the plugin and describe what you want:

```
@aholo-lux3d Use $lux3d to turn this request into verified 3D assets and deliver them into the current project.
```

Or simply reference the skill:

```
Use $lux3d to create verified 3D assets and one offline preview for this project.
```

---

## Repository layout

```
.
├── .agents/plugins/marketplace.json   # Codex marketplace manifest (source of truth)
└── plugins/
    └── aholo-lux3d/                   # the plugin package, contents unchanged
        ├── .codex-plugin/plugin.json  # plugin manifest
        ├── .codex-plugin/assets/      # logo, composer icon
        ├── skills/lux3d/              # SKILL.md, references, scripts, bundled runtime
        ├── adapter.json
        └── build-info.json
```

The plugin directory is a verbatim copy of the shipped Lux3D Codex release package.
Do not edit files inside `plugins/aholo-lux3d/` by hand; replace the directory with a
new build and bump `version` in `.codex-plugin/plugin.json`, then commit.

---

## Troubleshooting

**The plugin does not show up in Plugins.**
Run `codex plugin marketplace list` and confirm `aholo-lux3d` is listed with a resolved
root path. If it is missing, re-run `codex plugin marketplace add w77451493-creator/luxtest`.
If it is listed but the plugin is absent, run `codex plugin marketplace upgrade`.
Marketplace contents are cached, so a stale cache is the most common cause.

**I installed it but the agent still does not see it.**
Plugin capabilities are loaded when a task starts. Close the current task and open a new one.

**`CLI_DEPENDENCY_MISSING` when the plugin runs Python.**
Re-run `python3 <installed-skill>/scripts/setup_runtime.py` and retry with the interpreter
path it returns. A Python import failure does not mean the API key is invalid.

**The marketplace route is blocked (no access to GitHub / restricted environment).**
Fall back to the packaged release archive: download `lux3d-plugin-<version>.zip`, attach
it to a Codex task and ask the agent to install the plugin from the archive. Migration is
a matter of switching to the marketplace source once network access is available.

**Corporate proxy or mirror.**
`codex plugin marketplace add` accepts any Git URL, including an internal mirror:

```bash
codex plugin marketplace add https://<your-mirror>/<path>/luxtest.git --ref main
```

---

## Links

- Product site: https://labs.aholo3d.com
- Plugin manifest: [plugins/aholo-lux3d/.codex-plugin/plugin.json](plugins/aholo-lux3d/.codex-plugin/plugin.json)
- Skill entry point: [plugins/aholo-lux3d/skills/lux3d/SKILL.md](plugins/aholo-lux3d/skills/lux3d/SKILL.md)
