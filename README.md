# Aholo Lux3D

<!-- 介绍：这里写 2–3 句，说明 Lux3D 是做什么的、给谁用。写完把这段注释删掉。 -->

这是 Aholo Lux3D 的 Codex 插件市场源。用户直接从本仓库安装插件，**不需要下载 zip**。

| 项 | 值 |
| --- | --- |
| Marketplace | `luxtest` |
| 插件 | `aholo-lux3d` |
| 选择器 | `aholo-lux3d@luxtest` |
| 版本 | `0.1.0` |
| 分支 | `main` |

## 安装

把下面这句粘进 Codex 的任意任务：

```
/goal Read https://raw.githubusercontent.com/w77451493-creator/luxtest/main/AGENTS.md to install Aholo Lux3D for Codex and set up a new task for me.
```

中文版：

```
/goal 读 https://raw.githubusercontent.com/w77451493-creator/luxtest/main/AGENTS.md 帮我安装 Aholo Lux3D 插件，并新建一个任务。
```

装完**必须新建一个任务**——插件能力在任务启动时才加载，然后在任务里用 `$lux3d` 或 `@aholo-lux3d` 调用。

## 或者直接跑命令

```bash
codex plugin marketplace add w77451493-creator/luxtest --ref main
codex plugin add aholo-lux3d@luxtest
```

卸载：

```bash
codex plugin remove aholo-lux3d@luxtest
codex plugin marketplace remove luxtest
```

## 仓库内容

```
.agents/plugins/marketplace.json   Codex 市场清单，唯一配置入口
plugins/codex/aholo-lux3d/         插件本体，安装包原样，不要手改
AGENTS.md                          Agent 安装入口，prompt 读取的目标文件
```

发新版本时：替换 `plugins/codex/aholo-lux3d/` 整个目录，并**同步改 `.codex-plugin/plugin.json` 里的 `version`**。Codex 用 `marketplace/插件名/版本号` 当缓存 key，版本号不变就不会触发重装，用户永远停在旧版。

## 要求

- Codex CLI `0.121.0` 以上（或当前 Codex / ChatGPT 桌面端）
- Python 3.9+，命令为 `python3`（Windows 用 `python` / `py`）
- 计费生成需要 `LUX3D_CN_API_KEY`（国内）或 `LUX3D_GLOBAL_API_KEY`（海外）

插件不注册 MCP，也不需要额外下载任何东西。首次使用时会自动建一个私有 Python 环境装依赖（只有 `requests`），这一步不联网调 Lux3D、也不需要 API key。

## 注意

仓库必须保持 **public**。`codex plugin marketplace add` 走 GitHub 克隆，私有仓库对其他人会直接 404。
