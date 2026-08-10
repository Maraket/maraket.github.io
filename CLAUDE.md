<!-- nx configuration start-->
<!-- Leave the start & end comments to automatically receive updates. -->

# General Guidelines for working with Nx

- For navigating/exploring the workspace, invoke the `nx-workspace` skill first - it has patterns for querying projects, targets, and dependencies
- When running tasks (for example build, lint, test, e2e, etc.), always prefer running the task through `nx` (i.e. `nx run`, `nx run-many`, `nx affected`) instead of using the underlying tooling directly
- Prefix nx commands with the workspace's package manager (e.g., `pnpm nx build`, `npm exec nx test`) - avoids using globally installed CLI
- You have access to the Nx MCP server and its tools, use them to help the user
- For Nx plugin best practices, check `node_modules/@nx/<plugin>/PLUGIN.md`. Not all plugins have this file - proceed without it if unavailable.
- NEVER guess CLI flags - always check nx_docs or `--help` first when unsure

## Scaffolding & Generators

- For scaffolding tasks (creating apps, libs, project structure, setup), ALWAYS invoke the `nx-generate` skill FIRST before exploring or calling MCP tools

## When to use nx_docs

- USE for: advanced config options, unfamiliar flags, migration guides, plugin configuration, edge cases
- DON'T USE for: basic generator syntax (`nx g @nx/react:app`), standard commands, things you already know
- The `nx-generate` skill handles generator discovery internally - don't call nx_docs just to look up generator syntax

<!-- nx configuration end-->

<!-- personal configuration start-->
# Git & Documentation Practices

## Commits

- Commit at sensible cut points: each commit should be a complete, coherent
  unit of work (one feature, one fix, one refactor, one config change) that
  leaves the codebase in a working state. Don't bundle unrelated changes or
  commit broken intermediate states.
- Prefer several small, well-scoped commits over one large one.
- Use **Conventional Commits** for every message:

  ```
  <type>(<optional scope>): <short summary>

  <optional body: what changed and why>
  ```

  - Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`,
    `build`, `ci`, `chore`, `revert`.
  - Summary: imperative mood, lowercase, no trailing period, ≤72 chars.
  - Add a scope when it clarifies which part of the codebase changed,
    e.g. `feat(auth): add OAuth login flow`.
  - Use a `BREAKING CHANGE:` footer for breaking changes.
- Before running `git commit`, briefly state what changed and why, then
  write the commit message accordingly.

## Documentation

- Whenever new functionality is added (feature, module, endpoint, CLI
  command, config option, etc.), create or update matching documentation
  in `docs/`.
- If `docs/` doesn't exist, create it.
- Keep docs concise but complete: purpose, usage, relevant
  options/parameters, and a usage example where applicable.
- Follow existing file-naming conventions in `docs/`; if none exist, use
  `docs/<feature-name>.md`.
- Docs for a feature should either ship in the same commit as the feature
  (still typed `feat:`/`fix:`/etc.) or as an immediate follow-up commit
  typed `docs:`. Never leave new functionality undocumented.

## Planning

- All planning docs (roadmaps, architecture proposals, milestone
  breakdowns, design explorations) live in `plans/`, not `docs/`.
- `docs/` is for shipped functionality; `plans/` is for work not yet
  built or in progress.
- Follow existing `plans/` naming conventions (numbered prefix, e.g.
  `NN-topic.md`) and keep `plans/README.md` current as an index.
- Before starting a non-trivial feature or architectural change, write
  or update its plan in `plans/` first.
- When a planned feature ships, update the relevant `plans/` doc to
  reflect status (or fold its content into `docs/` and mark the plan
  entry as done) instead of leaving it silently stale.

## Progress Tracking

- Maintain a single live status doc at `plans/09-progress-tracker.md`.
  This externalises context so work can resume cleanly after any
  interruption (session end, crash, handoff).
- Structure: **Status** (what's shipped), **In Progress** (current
  task, files touched, approach), **Next Steps** (queued work, in
  order), **Blockers** (open questions, decisions needed).
- Update it at every commit cut point — don't let it drift stale.
  Overwrite in place; this is current state, not a changelog.
- At the start of a session (or after resuming from an interruption),
  read `plans/09-progress-tracker.md` first, before touching code.

## Review Loop

- Applies to non-trivial changes (new/changed logic, not docs-only,
  config-only, or typo-level edits).
- After implementing, before committing:
  1. Run the `dual-code-review` skill (`architecture-reviewer` +
     `security-reviewer`) against the diff.
  2. Zero `MANDATE` findings → proceed to commit. `SUGGEST` findings
     don't block; note them in the commit body or leave as a follow-up.
  3. Any `MANDATE` findings → fix them, then re-run the review on the
     updated diff. Repeat.
  4. Cap at 3 review rounds. If `MANDATE` findings remain after round 3,
     stop looping — surface the remaining findings to the user for a
     decision instead of forcing a commit or looping indefinitely.
- `.standards/` codification (per the `dual-code-review` skill) applies
  on every round, not just the last.

## Workflow Summary

1. Implement one logical change.
2. Update/add docs in `docs/` if functionality changed.
3. For non-trivial changes, run the Review Loop above until clean or
   capped.
4. Update `plans/09-progress-tracker.md` (status, next steps, blockers).
5. Commit with a Conventional Commits message.
6. Repeat for the next logical change.

<!-- personal configuration end-->