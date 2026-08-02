# Changelog

## 3.0.0

- Replaces the polling daemon with one-shot lifecycle hooks and a bounded reviewer connector.
- Moves ordinary patchset publication to hosted server work.
- Removes filesystem watching, Git polling, local spooling, runtime copying, and private update machinery.
- Binds publication, reviewer answers, media, and Push Changes to the exact authored session.

## 2.0.0

- Consolidated the Codex and Claude Code packages into one source tree.
- Made native plugin marketplaces responsible for installation and updates.
- Removed the secondary runtime downloader and cross-task activation protocol.
- Moved the publication tool to the OAuth-protected hosted MCP endpoint.
- Reduced lifecycle hook data to session and workspace metadata only.
- Kept one publication tool and the existing platform-neutral lifecycle.
