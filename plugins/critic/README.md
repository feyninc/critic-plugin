# Critic

Critic explains code changes from the coding-agent session that authored them.
It publishes a change narrative, one explanation for every changed file, and
optional range explanations for the parts that need more context. Reviewers can
then ask the authoring agent questions against the stable patchset.

## What the plugin installs

- One `explain-change` skill.
- One MCP tool named `critic.publish_patchset`.
- Four lifecycle hooks that connect an authoring session, observe its work, and
  request a publication checkpoint before the session finishes.
- One local bridge process that keeps device credentials, repository access,
  local snapshotting, and reviewer continuations on the user's device.
- One hosted OAuth MCP endpoint at `https://plugin.critic.run/mcp`.

The plugin does not review code, merge changes, push branches, open pull
requests, or write generated explanations into source files.

## Connection

Install Critic through the plugin directory for your coding agent. Sign in at
[critic.run](https://www.critic.run), open Connections, and follow the pairing
flow for Codex or Claude Code.

Codex requires explicit trust for command hooks. Open **Settings → Hooks** and
trust Critic's `SessionStart`, `UserPromptSubmit`, `PostToolUse`, and `Stop`
hooks before starting the authoring task.

Claude Code users in a managed environment may need an administrator to allow
`critic@claude-community` when `allowManagedHooksOnly` is enabled.

## Data and permissions

The local bridge reads Git metadata and the current patch in repositories where
the coding agent is already working. It sends the patch, explanations, selected
visual evidence, and Critic discussion context to Critic. Lifecycle hooks retain
only the event, session identifier, working directory, and relevant tool name.
They discard prompts, assistant messages, transcript locations, tool arguments,
and tool results before anything is spooled or transmitted. Device credentials
are stored under `~/.critic` with user-only permissions.

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
