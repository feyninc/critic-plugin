# Changelog

## 3.2.0

- Detects Codex shell and Git mutations through the native `exec_command` hook payload.
- Disables lifecycle work per task when a repository is not connected and rechecks after an explicit enable or repository change.
- Adds lightweight per-task on, off, and status controls without another MCP tool or background process.
- Keeps read-only tool hooks free of Git, network, connector, and task-state work.
- Binds renewed checkpoints to the ready local snapshot whenever the worktree still has unpublished edits, and retires each one-use token after publication.

## 3.1.0

- Moves repository observation to material PostToolUse events and makes ordinary Stop hooks constant-time local checks.
- Gives the authoring agent one hidden first-edit reminder and one bounded conditional adjudication per unpublished revision.
- Tracks local snapshots, commits, remote refs, GitHub patchsets, and pull requests as one change lineage.
- Adds optional agent attention requests to the publication tool and deduplicates them across local-to-remote promotion.
- Reduces the idle heartbeat to once every five minutes and removes focus-driven GitHub refreshes from the live dashboard.

## 3.0.1

- Declares the hosted publication result schema for reliable tool consumption and directory review.
- Matches the exact namespaced publication tool emitted by Codex and Claude Code.
- Marks the explanation skill as Codex-only and explicitly allows implicit invocation.
- Aligns package publisher metadata with the verified Chonkie, Inc. business identity.

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
