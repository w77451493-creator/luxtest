<p align="center">
  <img src="packages/aholo-lux3d/skill/aholo-lux3d/core/viewer/lux3d-logo.png" alt="Aholo Lux3D" width="420" />
</p>

# Aholo Lux3D

<p align="center">
  <strong>Languages:</strong>
  <a href="#english">English</a> ·
  <a href="#中文">中文</a> ·
  <a href="#日本語">日本語</a> ·
  <a href="#español">Español</a> ·
  <a href="#português">Português</a>
</p>

Install catalog for [Aholo Lux3D](https://lux3d.aholo3d.com). Turn a single image or text prompt into production-ready 3D assets (geometry, PBR materials, online preview, GLB export, API / ComfyUI).

This repository is shared by coding agents. One product has two parts: a Skill and an MCP Connector. Add the next product under `packages/` and `catalog.json`.

| | |
| --- | --- |
| Website | https://lux3d.aholo3d.com |
| Skill | `aholo-lux3d` |
| Connector | `aholo-lux3d-mcp` |
| Version | `0.1.2` |
| Branch | `main` |

---

## English

### What is Aholo Lux3D?

Aholo Lux3D generates accurate 3D geometry and complete PBR textures from one image or a text description. Preview models in the browser, export GLB, or integrate through API and ComfyUI for production workflows.

Website: https://lux3d.aholo3d.com

### Install

**One command (recommended)**

Paste into any coding-agent task:

```text
/goal Read https://raw.githubusercontent.com/w77451493-creator/luxtest/main/AGENTS.md and install Aholo Lux3D.
```

The agent installs both parts from this repository:

| Part | Directory | Role |
| --- | --- | --- |
| Skill | `packages/aholo-lux3d/skill/aholo-lux3d` | Local skill. Calls the Lux3D OpenAPI. |
| Connector | `packages/aholo-lux3d/connector/aholo-lux3d-mcp` | MCP instructions. The remote connection is registered separately. |

Importing the Connector folder does not connect MCP by itself. The agent also registers:

- Name: `Aholo Lux3D MCP`
- Transport: `streamable-http`
- URL: `https://api.aholo3d.cn/lux3d-mcp/mcp`
- Header: `Authorization`
- Value: the China-region Lux3D API key, with no `Bearer` prefix

After install, start a **new** task. Skills load when a task starts, so an existing task will not see them. Paid generation needs `LUX3D_GLOBAL_API_KEY`.

### Check before you install

If `aholo-lux3d` or `aholo-lux3d-mcp` is already installed at `0.1.2`, keep that copy. Do not install a second one. An older copy should be replaced, not left enabled beside the new one.

---

## 中文

### Aholo Lux3D 是什么？

Aholo Lux3D 可将单张图片或文字描述转为可用于生产的 3D 资产：准确几何、完整 PBR 材质、在线预览、GLB 导出，并支持 API / ComfyUI 接入。

- 中国站：https://lux3d.aholo3d.cn
- 国际站：https://lux3d.aholo3d.com

### 安装

**一条指令（推荐）**

在任意 Coding Agent 任务中粘贴：

```text
/goal Read https://raw.githubusercontent.com/w77451493-creator/luxtest/main/AGENTS.md and install Aholo Lux3D.
```

Agent 会从本仓库安装两部分：

| 部分 | 目录 | 作用 |
| --- | --- | --- |
| Skill | `packages/aholo-lux3d/skill/aholo-lux3d` | 本地技能，调用 Lux3D OpenAPI |
| Connector | `packages/aholo-lux3d/connector/aholo-lux3d-mcp` | MCP 说明。远程连接要另外注册 |

只导入 Connector 目录不算已经连上 MCP。Agent 还会注册：

- 名称：`Aholo Lux3D MCP`
- 传输：`streamable-http`
- 地址：`https://api.aholo3d.cn/lux3d-mcp/mcp`
- 认证头：`Authorization`
- 值：中国站 Lux3D API Key，不加 `Bearer`

安装完成后，请**新建**任务。技能在任务启动时才加载，已经在跑的任务看不到它。付费生成使用 `LUX3D_CN_API_KEY`（国内）或 `LUX3D_GLOBAL_API_KEY`（国际）。

### 安装前先确认

如果 `aholo-lux3d` 或 `aholo-lux3d-mcp` 已经是 `0.1.2`，沿用已有那份，不要再装第二份。旧版本应替换，不要和新版本同时启用。

---

## 日本語

### Aholo Lux3D とは？

Aholo Lux3D は、1 枚の画像またはテキストから、正確なジオメトリと完全な PBR テクスチャを持つ本番向け 3D アセットを生成します。ブラウザでプレビューし、GLB を書き出し、API / ComfyUI で連携できます。

ウェブサイト：https://lux3d.aholo3d.com

### インストール

**1 行コマンド（推奨）**

任意の Coding Agent のタスクに貼り付け：

```text
/goal Read https://raw.githubusercontent.com/w77451493-creator/luxtest/main/AGENTS.md and install Aholo Lux3D.
```

Agent は Skill（`aholo-lux3d`）と Connector（`aholo-lux3d-mcp`）の両方をインストールします。Connector のフォルダを置いただけでは MCP は接続されません。接続先は `https://api.aholo3d.cn/lux3d-mcp/mcp`、認証ヘッダーは `Authorization`、値は中国向け API キー（`Bearer` なし）です。

インストール後は**新しい**タスクを開始してください。有料生成には `LUX3D_GLOBAL_API_KEY` が必要です。すでに `0.1.2` がある場合は、二つ目を追加しないでください。

---

## Español

### ¿Qué es Aholo Lux3D?

Aholo Lux3D convierte una imagen o una descripción de texto en activos 3D listos para producción: geometría precisa, texturas PBR completas, vista previa en el navegador, exportación GLB e integración por API / ComfyUI.

Sitio web: https://lux3d.aholo3d.com

### Instalar

**Un comando (recomendado)**

Pega esto en cualquier tarea del agente:

```text
/goal Read https://raw.githubusercontent.com/w77451493-creator/luxtest/main/AGENTS.md and install Aholo Lux3D.
```

El agente instala la Skill (`aholo-lux3d`) y el Connector (`aholo-lux3d-mcp`). Importar solo la carpeta del Connector no conecta el MCP. La conexión es `https://api.aholo3d.cn/lux3d-mcp/mcp`, con el encabezado `Authorization` y la clave de API de China, sin `Bearer`.

Después, abre una **nueva** tarea. La generación de pago requiere `LUX3D_GLOBAL_API_KEY`. Si la versión `0.1.2` ya está instalada, no añadas una segunda copia.

---

## Português

### O que é o Aholo Lux3D?

O Aholo Lux3D transforma uma imagem ou um texto em ativos 3D prontos para produção: geometria precisa, texturas PBR completas, pré-visualização no navegador, exportação GLB e integração via API / ComfyUI.

Site: https://lux3d.aholo3d.com

### Instalar

**Um comando (recomendado)**

Cole em qualquer tarefa do agente:

```text
/goal Read https://raw.githubusercontent.com/w77451493-creator/luxtest/main/AGENTS.md and install Aholo Lux3D.
```

O agente instala a Skill (`aholo-lux3d`) e o Connector (`aholo-lux3d-mcp`). Importar só a pasta do Connector não conecta o MCP. A conexão é `https://api.aholo3d.cn/lux3d-mcp/mcp`, com o cabeçalho `Authorization` e a chave de API da China, sem `Bearer`.

Depois, abra uma **nova** tarefa. A geração paga precisa de `LUX3D_GLOBAL_API_KEY`. Se a versão `0.1.2` já estiver instalada, não adicione uma segunda cópia.
