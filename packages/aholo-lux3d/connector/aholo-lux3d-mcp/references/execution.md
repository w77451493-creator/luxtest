# Execution and recovery through MCP

Before submitting, establish the actual connection and identity as described in
[MCP workflow](../body.md), confirm each file input has a successful
[unified-upload receipt](upload.md) and uses its returned URL, obtain a current matching
quote and apply [Review and approval](review.md). The base package's unverified
qualification flags do not grant permission to bypass host/endpoint acceptance.

Use a stable operation ID and retain the exact plan digest, account isolation
reference, region, source, normalized Agent name, connector mode, quote validity
and task ID when known. Keep task IDs as decimal strings to avoid numeric
precision loss. Where available, persist these records in private host state,
separate from portable deliverables. A stored `approved=true` or copied budget
ledger is not conversation authorization. When automatic execution is authorized,
one coordinator must reserve its quoted budget before parallel dispatch. If
durable tracking is unavailable, disclose the limitation and serialize work;
stop new spending if authorization or prior attempts cannot be reconciled.

Track planned, quoted, authorized, submitting, submitted and completed/failed
stages. Mark a timeout or ambiguous response during creation as
`submission-unknown`, preserve its commitment and reconcile before any further
attempt. Submit each exact quoted create request once. Without verified server
idempotency, never automatically retry a create call over the network, another
endpoint or the other mode. `uniqueId` does not provide idempotency. Client or
instruction locks cannot guarantee exactly-once execution across devices.

Use `gettask` for a known task ID and `get_listtasks` to find reliable records for
the authenticated account. Matching a prompt or filename alone cannot identify
an uncertain submission. Preserve the original identity, account and mode when
recovering; if evidence is inconclusive, pause new creation and report that state.
Do not interpret a query timeout as a failed remote task. Report cancellation or
refund only when the service actually confirms it.

Follow the installed descriptor's request and polling limits: one create attempt,
at most three attempts for a read-only operation, bounded backoff and polling.
Quote uses POST and is not covered by automatic read-only retry. Honor host
response/download limits. A polling or size limit pauses local work and leaves
the task recoverable; it does not mean remote failure. Never change regions to
work around an error. Failed local delivery resumes delivery only.

For delivery, use genuine artifact URLs returned by task results, or download
through an available host tool and verify its actual local output. Temporary
URLs may expire. Do not represent remote filesystem paths as local files.
Check the live tool schema and returned asset metadata for available model
formats; unsupported output formats cannot be inferred from a ZIP. Preserve
source models and identify partial success honestly.
The shared review's mention of output-format helpers applies only when the host
actually provides such a helper. This Connector bundles none; use the live
schema and returned metadata above instead of looking for a missing script.

Offline preview, Blender assembly, scene rendering and local inspection depend
on available host capabilities. Do not promise these outputs unless the host can
produce and verify them. This package includes an optional identity helper, but
does not bundle local 3D execution or a viewer.
Diagnose failures with redacted error codes, mode, resolved host, region and operation
reference; keep credentials, signed URLs and other users' records out of logs.
