---
name: aholo-lux3d-mcp
description: Use Aholo Lux3D MCP for image generation or reference-based image editing, 3D assets, materials, exports and task recovery. Use when the user selects Aholo Lux3D MCP, explicitly requests its tools, or needs to connect the MCP integration from a native plugin or a downloaded Connector. Check the actual tools before executing.
---

# Aholo Lux3D MCP

When this Skill is selected or the user requests Aholo Lux3D, execute the requested
operation through **Aholo Lux3D MCP**. Aholo Lux3D supports **2D image operations as well as
3D assets**. Do not silently replace it with a host's image editor, Seedream,
another image model or another provider because a tool or file is missing.
Report the specific missing capability and help connect Aholo Lux3D. Use an alternative
only if the user chooses it, and name the provider actually used.

## First use: find the tools, then verify the connection

This Skill is shared by native ecosystem MCP plugins and the public-portal
Connector. A native installer may register the connection; importing a Skill
ZIP alone **does not automatically register or authenticate a remote MCP server
in every host**. Check and reuse a working connection before changing settings.
A Skill label in the conversation is not proof that its tools are connected.

1. Inspect this session's tool list. If the host supports deferred tool discovery
   (for example a tool-search facility), search for `Aholo Lux3D MCP`, `Aholo Lux3D`, `lux3d-mcp`, the
   required tool names below, and their task descriptions. Use the callable
   identifiers the host returns; it may add a namespace or display label.
   Check that their server provenance is the intended Aholo Lux3D connection.
2. For new generation, confirm account, quote, the selected create tool and
   `gettask` are callable and inspect their input schemas. For recovery, discover
   only the relevant query tools. A missing unrelated operation does not disable
   a supported one. **Perform discovery even if a local JSON file is missing.**
   Missing documentation does not prove that the remote server is disconnected.
3. If the needed tools are absent, the task has not started. Give the connection
   settings below. Use the host's supported MCP registration facility if it is
   available and the user's existing credential is securely configured;
   otherwise guide the user to the host's MCP connection settings. Do not invent
   a menu or claim that another ZIP import establishes a connection. If this
   client cannot register remote MCP, state that specific limitation.
4. After connection/reconnection, discover again. For new work, resolve host
   identity as below and call `getlux3daccountbalance` with the actual schema.
   Only a successful response verifies this session's authentication/account
   access; do not treat a timeout as a bad key. This account check does not create
   a generation task. Then proceed to inputs, plan, quote and authorized creation.

The connection settings are in this entry so tool discovery and setup do not
depend on finding a parent directory:

| Setting | Value |
| --- | --- |
| Connection display name | **Aholo Lux3D MCP** |
| Server key, where supported | `lux3d-mcp` |
| Transport | Streamable HTTP (`streamable-http`) |
| Remote URL | `https://api.aholo3d.cn/lux3d-mcp/mcp` |
| Authentication | User's **China-region** Aholo Lux3D API Key in the raw `Authorization` header; **no `Bearer` prefix** |
| Get a key | [Aholo Lux3D API Key page](https://labs.aholo3d.cn/api-keys) |

Store the key in the host's private connection settings. Never request it in
chat or write it into this package. This URL is an MCP transport endpoint, not
an image URL or a JSON REST endpoint for directly posting arbitrary tool names.
Typing a tool name in a reply is not invoking it.

If only this Skill was imported, a useful status is: “Aholo Lux3D 指引已加载，但本次会话
尚未发现所需 MCP 工具。请在宿主的 MCP 连接设置中添加上述地址和国内 API Key，
连接后我会重新发现工具并检查账户；当前尚未调用 Aholo Lux3D，也未改用其他生成服务。”
Use this only when discovery actually finds no required tools.

## Route the request to the correct Aholo Lux3D tool

These are expected server tool names, not a substitute for the live schemas.
Match the discovered callable and read its required arguments, reference-input
fields and body/envelope before calling; never guess a `prompt`, image field or
outer `body` shape when the schema is available.

| Task / operation | Expected tool | How to use it |
| --- | --- | --- |
| `account` | `getlux3daccountbalance` | Read current account facts and the quote `uniqueId`. |
| `quote` | `post_quotelux3dopenapirequests` | Price the numbered plan of canonical OpenAPI create requests. |
| `multimodal-image` | `post_createmultimodaltoimagetask` | **2D** image generation or reference-based image changes using the discovered text/image inputs; inspect this for hair, clothing or background edits. |
| `four-view` | `post_createimagetofourviewtask` | Create four views when the requested plan needs them. |
| `image-to-3d` | `post_createimgto3dtask` | Create a 3D asset from prepared image inputs. |
| `text-to-3d` | `post_createtextto3dtask` | Create a 3D asset from a text description. |
| `material-transfer` | `post_creatematerialtransfertask` | Apply a requested material change to a model. |
| `multi-format-export` | `post_createmultiformatexporttask` | Convert/export a model to supported target formats. |
| `get-task` | `gettask` | Query a returned Aholo Lux3D task ID and retrieve real result URLs. |
| `list-tasks` | `get_listtasks` | List this account's tasks for discovery or recovery. |

For “把头发换成红色长卷发，重建图片里的场景”, inspect the multimodal **image**
tool when the intended result is an edited picture; do not conclude that Aholo Lux3D
only supports GLB/OBJ/FBX. If “重建场景” could mean an editable 3D asset, clarify
that deliverable before quoting a different workflow. Preserve the subject and
requested changes. A 2D image is not evidence that a 3D scene was reconstructed.
If the discovered tool does not support the needed image inputs, report that
specific limitation without silently choosing another provider.

For an explicit “先用 Aholo Lux3D 改图，再做场景/3D 重建”, plan both requested stages:
`post_createmultimodaltoimagetask → gettask → edited image → unified Asset/OUS
upload → post_createimgto3dtask → gettask`. Use actual supported schema fields
and quote/authorize each intended stage, using staged quotes when the next input
depends on the first result. Do not invent the edited URL before task completion.
Retain the edit result if the 3D stage is blocked, and report partial completion;
do not present the edited picture alone as the requested 3D result.

## Execute the chosen operation

1. Identify the requested deliverable and selected Aholo Lux3D operation. Prepare all
   file inputs through the unified upload below; preserve their order and role.
2. Use the verified account context and [tool map](tool-map.json) to build a
   numbered plan. Quote the **canonical `/lux3d/v1/...` paths**, not MCP tool names.
   Follow [Planning and quotes](references/planning.md) for parameter encoding.
3. Show the actual returned quote and apply [Review and approval](references/review.md).
   Reuse existing authorization within its scope; choosing a Connector alone
   does not introduce another confirmation requirement. Unknown prices are not free.
4. Invoke the selected discovered create tool once. Record the real returned
   task ID as a string immediately; creation accepted is not task completion.
5. Query `gettask` until completion or the bounded wait expires, following
   [Execution and recovery](references/execution.md). Return actual result URLs
   and truthful status. Do not retry an uncertain create or switch providers to
   conceal its failure. Do not claim a Aholo Lux3D result without a Aholo Lux3D task/result.

## Upload every file input through Asset/OUS

Upload is supported through the public Asset API, **not** one of the ten MCP
tools: `GET /asset/v1/token → OUS upload → successful status URL`. It uses the
**same China-region API Key as MCP**, securely injected into the Asset request;
MCP login alone does not expose the stored secret to an HTTP tool.

Local files are uploaded; external and host-attachment URLs must first be
downloaded and then uploaded through this same chain. Only a completed unified
upload URL or a matching valid upload receipt may enter Aholo Lux3D input fields.
An unrelated “upload file” tool returning a public URL is not sufficient.
Compute whole-file MD5 first, use the token's `blockSize` for single/part upload,
and wait for `status=5` and a real returned URL. Read
[Unified input upload](references/upload.md) for exact fields and credentials.
If the host lacks this upload capability, report it before the affected create;
never pass the original URL through as a workaround. Final output links sent to
the user do not require re-upload unless they become another operation's input.

## Host identity and package files

Use the real current host, not the model vendor: Codex=`1/codex`, Claude Code=
`2/claude-code`, DeepSeek=`3/deepseek`, WorkBuddy=`4/workbuddy`; other hosts use
`100` and their real name. Thus a 豆包 session uses `source=100, agentName=豆包`.
Use [host-identity.json](host-identity.json) for aliases, or the optional
[identity helper](scripts/host_identity.py). Source 100 needs the same real name
on account and quote; known hosts use the canonical name on quote. Check that
the live schemas or the host integration actually accept/inject these fields.
No user-selected profile or installation binding is needed.

Keep the **whole `aholo-lux3d-mcp/` Skill directory** installed. A native plugin
may place it under its own Skills directory; the public-portal Connector uses
it as the ZIP root. `SKILL.md`, `connection.json`,
`tool-map.json`, `host-identity.json`, `body.md`, `references/` and `scripts/` are
in this same Skill root. Resolve paths from this Skill's location, not
the working directory; there is no dependency on a parent plugin folder.
These shared files describe how to connect; an ecosystem wrapper may separately
provide its native MCP registration, which must still be verified in this session.

The installed Skill name is `aholo-lux3d-mcp`, so hosts that derive their visible
name from frontmatter also retain the Aholo prefix. This differs from the remote
server key `lux3d-mcp`; do not rename server tools, endpoints or host attribution.

If the host imported only this Markdown and omitted resources, retain the setup
settings and tool routing above, discover actual tools, and report the incomplete
Skill installation separately. Restore required supporting files before an
operation that needs their protocol; do not pretend to have read missing files
or infer server state from their absence. See [Installation](README.md) and the
[MCP workflow](body.md) for the detailed checks. Communicate in the user's language.
