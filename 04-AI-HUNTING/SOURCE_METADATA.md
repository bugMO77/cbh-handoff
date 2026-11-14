# SOURCE_METADATA.md — Ai-Hunting

## Repository Identification

| Field | Value |
|-------|-------|
| Repository URL | https://github.com/0xmannaf/Ai-Hunting |
| Owner | 0xmannaf |
| Repository name | Ai-Hunting |
| Default branch | main |
| Pinned commit SHA | `3c1e9a021779eeffbd2c021b8664aa24c1df04b2` |
| Commit date (verified with `git log -1`) | 2026-10-06T18:42:40+03:00 |
| Commit subject | "Initial commit" |
| Inspection date | 2026-11-04 |
| License | **NO LICENSE FILE FOUND** — no OSI licence declared |
| Permission context | See `CREATOR_PERMISSION_CONTEXT.md` |
| Snapshot | `source-snapshot/` (154 files, curated) |
| Curation record | See `SNAPSHOT_CURATION.md` |

## Repository Description

> "A curated list of AI models I use for bug bounty hunting, security research, recon, analysis, and automation."

(Auto-derived description shown by the GitHub API for the repository.)

## Repository Metrics (as observed at inspection)

| Metric | Value |
|--------|-------|
| Stars | 29 |
| Watchers | 0 |
| Forks | 8 |
| Files tracked at pinned commit | 312 |

These counts are point-in-time observations and may change.

## Verification Method

- **Full clone** of the public repository (not a shallow clone) followed by checkout of the
  pinned commit.
- `git rev-parse HEAD` confirmed `3c1e9a021779eeffbd2c021b8664aa24c1df04b2`.
- `git log -1` confirmed the commit date and subject.
- Static inspection only. **No code was executed.**
- No repository files were modified.

## Key Files Inspected

| File | Size | Purpose | Evidence status |
|------|-----:|---------|-----------------|
| `AGENTS.md` | 12,830 B | Master directives | Content read |
| `agent-briefing.md` | 10,563 B | Knowledge-state briefing | Content read |
| `prioritization.md` | 18,182 B | P1–P4 prioritisation framework | Content read |
| `prompts.md` | 120,419 B | Prompt library | Partially read |
| `package.json` | 452 B | Node/Playwright config | Content read |
| `.opencode.json` | — | MCP + browser config | Content read |
| `opencode.json` | 540 B | OpenCode agent config | Content read |
| `runtime/registry.json` | 14,475 B | Canonical agent/skill registry (6 agents) | Parsed |
| `runtime/opencode/ORCHESTRATION.md` | 11,639 B | Orchestration manual | Read |
| `runtime/opencode/agents/*.md` | 11 files | Agent briefs (two conflicting sets) | Read |
| `learning_engine/engine.py` | 13,809 B | Learning engine public API | Read |
| `learning_engine/retrieval/search.py` | 3,178 B | Retrieval implementation | Read |
| `learning_engine/graph/builder.py` | 1,878 B | Graph export | Read |
| `skills/*.md` / `.agents/skills/*/SKILL.md` | 22 pairs | Skill playbooks | Enumerated + spot-read |
| `.github/workflows/*.yml` | 2 files | CI workflows | Read |

## Snapshot Contents Summary

- 154 of 312 tracked files included.
- Excluded: `.git/`, `testing/` (157 files of sensitive target evidence),
  `scripts/__probe__/` (1 binary DB).
- Preserves original repository paths under `source-snapshot/`.

## Limitations

1. **No LICENSE file** — no OSI licence declared; creator video statements are permission
   context only, not a licence. See `CREATOR_PERMISSION_CONTEXT.md`.
2. **No runtime testing** — all findings are from static inspection.
3. **Tests not executed** — test files and CI workflow definitions exist, but no local run
   was performed and no CI run evidence for this commit was retrieved.
4. **Two conflicting agent taxonomies** exist in the repository (see architecture report).
5. **Third-party component licensing unresolved** — some content appears derived from books,
   labs, and external sources; their licence status is unknown to this package.
6. **Commit-count/contributor data** not analysed beyond the pinned commit.

## Source Reference

- Repository: https://github.com/0xmannaf/Ai-Hunting
- Commit: `3c1e9a021779eeffbd2c021b8664aa24c1df04b2`
- Inspected: 2026-11-04
