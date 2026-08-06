# Critic

Critic explains code changes from the coding-agent session that authored them.
It publishes a change narrative, one explanation for every changed file, and
optional range explanations for the parts that need more context. Reviewers can
then ask the authoring agent questions against the stable patchset.

## What the plugin installs

- One `explain-change` skill.
- One MCP tool named `critic.publish_patchset`.
- Three lifecycle hooks that connect an authoring session, observe its work, and
  request a publication checkpoint before the session finishes.
- One Node runtime containing short-lived lifecycle hooks and a bounded
  outbound reviewer connector.
- One hosted OAuth MCP endpoint at `https://plugin.critic.run/mcp`.

The plugin does not review code, merge changes, push branches, open pull
requests, or write generated explanations into source files.

## Connection

Install Critic through the plugin directory for your coding agent. Sign in at
[critic.run](https://www.critic.run), open Connections, and follow the pairing
flow for Codex or Claude Code.

Codex requires explicit trust for command hooks. Open **Settings → Hooks** and
trust Critic's `SessionStart`, `PostToolUse`, and `Stop`
hooks before starting the authoring task.

Claude Code users in a managed environment may need an administrator to allow
`critic@claude-community` when `allowManagedHooksOnly` is enabled.

## Data and permissions

Lifecycle hooks read Git metadata and the current patch only in repositories
where the coding agent is already working. They send the patch, explanations,
selected visual evidence, and Critic discussion context to Critic. They retain
only the event, session identifier, working directory, and relevant tool name.
Prompts, assistant messages, transcript locations, tool arguments, and tool
results are discarded. There is no local spool, Git poller, filesystem watcher,
runtime copy, or private updater. Device credentials are stored under
`~/.critic/v3` with user-only permissions.

The reviewer connector holds one outbound Convex websocket and a five-minute
heartbeat while connected. Idle heartbeats do not run Git, scan files, or grow
local state. Reviewer conversations use the exact authored session and expose
only Critic's repository-scoped read tools. Critic never reads coding-agent
transcripts.

The publication tool writes to Critic and may replace or delete existing
explanations when the caller explicitly requests those operations. It does not
change GitHub code or repository state.

See the [privacy policy](https://www.critic.run/privacy) and
[terms](https://www.critic.run/terms).

## Support

Email [support@usefeyn.com](mailto:support@usefeyn.com) or visit
[critic.run/support](https://www.critic.run/support). The reviewable plugin
package is mirrored at
[github.com/feyninc/critic-plugin](https://github.com/feyninc/critic-plugin).
