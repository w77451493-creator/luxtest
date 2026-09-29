# luxtest

给 Coding Agent 用的共用安装目录。一个仓库可以放多个产品。每个产品有两部分：Skill，以及 MCP Connector。

当前产品是 Aholo Lux3D `0.1.2`。

| 部分 | 目录 | 作用 |
| --- | --- | --- |
| Skill | `packages/aholo-lux3d/skill/aholo-lux3d` | 本地技能，走 Lux3D OpenAPI |
| Connector | `packages/aholo-lux3d/connector/aholo-lux3d-mcp` | MCP 说明。远程连接要另外注册 |

## 安装

在当前 Coding Agent 的任务里粘贴：

```text
/goal Read https://raw.githubusercontent.com/w77451493-creator/luxtest/main/AGENTS.md and install Aholo Lux3D.
```

Agent 会按 `AGENTS.md` 安装 Skill 和 Connector，并单独注册这条 MCP：

- 地址：`https://api.aholo3d.cn/lux3d-mcp/mcp`
- 认证头：`Authorization`
- 值：中国站 Lux3D API Key，不加 `Bearer`

只导入 Connector 目录不算已经连上 MCP。

直接下载：

- [Skill zip](packages/aholo-lux3d/dist/lux3d-plugin-0.1.2-common-skill.zip)
- [Connector zip](packages/aholo-lux3d/dist/lux3d-plugin-0.1.2-common-connector.zip)

## 再加一个产品

在 `packages/<产品名>/` 放下一个 Skill 目录和一个 Connector 目录，然后在 `catalog.json` 加一条。不要为每个产品新建仓库。
