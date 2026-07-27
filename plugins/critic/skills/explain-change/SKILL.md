---
name: explain-change
description: Use when Critic schedules an explanation checkpoint for the current workspace, or when the user asks to publish, update, delete, or improve Critic explanations.
---

# Explain the current patchset in Critic

Treat Critic as the understanding layer for agent-written code. It does not review or gate merges.

## At a scheduled checkpoint

Stay in the authoring conversation that wrote the change. Do not fork or reconstruct intent in a fresh conversation. Read the exact current workspace diff and call `critic.publish_patchset`. Critic deterministically targets the matching GitHub pull-request patchset when one exists; otherwise it publishes an owner-only local change. Do not push, open a pull request, or change Git state merely to make Critic work.

For a first publication, provide:

1. One concise change narrative in Markdown with required `incoming` (“Before”) and `outgoing` (“After”) boundaries. The supporting body may be empty when the boundaries already tell the whole story.
2. One useful file narrative for every changed path, including tests, configuration, generated files, vendored files, and lock files.
3. Range explanations only at semantic cliffs: non-obvious invariants, lifecycle or concurrency boundaries, security or data-loss edges, compatibility shims, algorithmic tradeoffs, or intent that cannot be read honestly from the code.

Write for a reader who is scanning. Lead with concrete behavior. Use as many complete sentences as the explanation needs, but give every sentence a distinct purpose and remove repetition. Prefer active voice and familiar words. Avoid canned transitions, generic benefit claims, em dashes, en dashes, colons, and semicolons in prose. Do not create fragments merely to make an explanation shorter. Technical punctuation inside code spans, URLs, commands, and paths is allowed.

Never explain syntax or place Critic text in source files, commit messages, or GitHub comments. Adapt density to the reader’s familiarity and involvement. State uncertainty rather than inventing intent.

## Updating explanations

`critic.publish_patchset` is an incremental upsert. Include only explanations that need to be added or changed; omitted explanations and their discussion threads remain intact. Use `deleteExplanations` in the same tool only for explanations that should be removed. A new patchset must still end with one current change narrative and one current file narrative for every changed path.

## Preview information

Only the change narrative may include preview information:

- `sharedPreviewUrl`: an independently accessible HTTP(S) team deployment. Never put localhost or another machine-local address here.
- `localPreviewInstructions`: concise, verified Markdown instructions for reproducing or previewing the change locally.

Include either, both, or neither based on whether they help. Do not invent or guess them.

## Visual evidence

For meaningful UI, styling, responsive layout, interaction, animation, visualization, or rendering changes, inspect the integrated product after implementation and attach representative evidence to the change narrative.

- Prefer three to six high-signal screenshots for materially different changed states.
- Use a short video only when motion is the behavior.
- Use self-contained interactive HTML only when a system or spatial relationship is genuinely clearer interactively.
- Open and inspect every capture before publication.
- Provide concise alt text and captions.
- Pass local evidence through the change narrative’s `media` field. Do not merely mention a path in prose.
- Never attach stale, broken, duplicate, placeholder, or fixture captures.

If the product cannot be run, say why rather than fabricating evidence. Diagrams remain optional; use fenced Mermaid only when several actors, ownership boundaries, or state transitions are materially harder to explain linearly.

## Verify and hand off

Before publishing, confirm the current workspace, changed paths, and anchors. After publication, open the returned canonical Critic URL and verify the narrative, file coverage, and media render. End the final response with a standalone `Critic: <returned URL>` line and use it instead of the GitHub URL as the primary handoff.

Reviewer questions are separate. Critic may fork the stable authoring context to answer them, but those forks never own the initial authoring checkpoint.
