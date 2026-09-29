# Aholo Lux3D MCP

These shared MCP instructions, connection descriptor and tool map are used by
both the public-portal Connector and native ecosystem MCP plugins. Their wrappers
provide host-specific packaging, registration and installation metadata; the
business workflow and tool rules remain the same. The public portal supplies one
universal Connector ZIP; native ecosystem releases may publish their own packages
to their marketplaces. Users do not select a profile or edit source attribution.

## Install locally

**Loading this Skill and connecting its remote MCP are separate capabilities.**
A native plugin installer may configure both, while importing the public-portal
ZIP as a Skill can load only the instructions. These shared files do not assume
one vendor's registration format or menu. If an authenticated Aholo Lux3D connection
already exists, verify and reuse it; do not create a duplicate connection.

1. In the host's MCP connection settings, add a remote Streamable HTTP connection
   displayed as **Aholo Lux3D MCP**, using server key `lux3d-mcp` where supported,
   with URL `https://api.aholo3d.cn/lux3d-mcp/mcp`.
2. Obtain your China Aholo Lux3D API Key from the
   [API Key page](https://labs.aholo3d.cn/api-keys). Put the raw key in the host's
   private `Authorization` header or credential setting, without a `Bearer`
   prefix. Do not paste the key into chat or commit it to this package. A host
   must support this header and isolate it per user connection.
3. Keep the **whole `aholo-lux3d-mcp/` Skill directory**, whose root contains
   [SKILL.md](SKILL.md), `connection.json`, `tool-map.json`, `host-identity.json`,
   `body.md`, `references/` and `scripts/`. Do not import only the Markdown file.
   A native plugin may install this directory under its own Skills directory;
   the public-portal Connector puts it at the ZIP root. Read these files relative
   to `SKILL.md`, with no runtime dependency on the source repository. If the host only loads instruction
   text, it still needs access to the supporting documents for the relevant
   operation, as well as a separately registered remote MCP connection.
4. Reconnect and discover the tools. Check their schemas against
   [tool-map.json](tool-map.json) and verify the account/quote identity arguments
   described in [the workflow](body.md). Perform a non-billable account check
   with the resolved identity. Report the connection ready only after actual
   discovery and successful authentication; do not create a task as a test.

After importing, a useful first request is: “使用 Aholo Lux3D MCP。先发现并检查 Aholo Lux3D
工具和账户；没接通就给出连接步骤，不要改用别的图片生成工具。” The agent should
inspect available/deferred tools rather than decide connection status from the
existence of local JSON files. Missing files mean an incomplete instruction
installation; absent tools mean this session has not exposed those operations.

The entry lists all ten tool routes, including 2D image generation/editing via
`post_createmultimodaltoimagetask`. Aholo Lux3D is not limited to 3D model output. If
the user selects Aholo Lux3D and a needed tool is unavailable, report the missing
capability; do not silently switch to a host image model or another provider.

[connection.json](connection.json) is a vendor-neutral descriptor of these same
settings, not a JSON file guaranteed to import into every host. Different hosts
have different configuration formats; use their supported local UI or config
format, preserving the URL, raw authorization and supplied instructions. This
package does not substitute an unverified international MCP endpoint.

## Prepare file inputs through the unified upload

Every input file URL passed to Aholo Lux3D must come from the unified Asset/OUS upload.
For a local attachment, upload its bytes. For an external URL (including another
host uploader's URL), download the file first, then use that same Asset/OUS
flow. Only use the `url` returned by successful upload status, or reuse a matching
completed upload receipt. An externally accessible URL may be unreadable by
Aholo Lux3D's internal services and must not be passed through directly.

Read [Unified input upload](references/upload.md) for the exact
token, whole-file MD5, dynamic block-size, multipart and status steps. The ten
MCP tools do not expose upload. This Asset path uses the same China-region
Aholo Lux3D API Key as the MCP connection; no separate upload key is required.
The host needs either this specific upload
integration or file/HTTPS tools with supported secure credential injection.
Connecting MCP alone does not make its secret available to those tools. If a
required capability is missing, configure it through the host before creating
the affected task; do not fall back to submitting the original URL. Account,
quote, generation and task operations continue through MCP after preparation.

## Automatic host identity

The host obtains its real name from the current session and resolves it through
[host-identity.json](host-identity.json). The optional Python helper is
[scripts/host_identity.py](scripts/host_identity.py). Hosts without Python apply
the same registry rules themselves; no separate download or implementation is
required. Users never select an ecosystem or manually assign `source`.

| Actual running host | source | agentName |
| --- | --- | --- |
| Codex | 1 | `codex` |
| Claude Code | 2 | `claude-code` |
| DeepSeek | 3 | `deepseek` |
| WorkBuddy | 4 | `workbuddy` |
| Another host, for example 豆包 | 100 | Actual trimmed host name, for example `豆包` |

Known host aliases compare without case sensitivity. Unknown names preserve
case after trimming; blank names, controls, surrogates and names over 128
characters are invalid. Account calls require the real name for source 100;
quotes require it for every source. Derive these request parameters from the
session for each installation; never hard-code one host into these shared files.

This shared layer defines portable contents and installation steps. Whether a
particular Codex, DeepSeek or 豆包 client/version supports local Skills, remote
MCP, custom authentication and identity forwarding must be checked against that
client and the ecosystem wrapper being installed. Shared contents alone do not
prove native installation or live connector acceptance. Preserve the qualification
state in the descriptor and verify the
affected integration before billable creation.
