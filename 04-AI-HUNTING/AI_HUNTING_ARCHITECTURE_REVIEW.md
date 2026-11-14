# AI_HUNTING_ARCHITECTURE_REVIEW

**Repository:** https://github.com/0xmannaf/Ai-Hunting
**Owner:** 0xmannaf
**Default branch:** main
**Pinned commit:** `3c1e9a021779eeffbd2c021b8664aa24c1df04b2`
**Commit date (verified locally via `git log -1`):** 2026-10-06T18:42:40+03:00
**Commit subject:** "Initial commit"
**Inspection date:** 2026-11-04
**Method:** static file inspection of a full clone at the pinned commit. No code executed.
**License:** No LICENSE file found. Creator video statements are recorded separately in
`CREATOR_PERMISSION_CONTEXT.md`; they are permission context, not an OSI licence.

---

## Evidence status vocabulary

Every maturity statement below uses one of:

| Label | Meaning |
|-------|---------|
| `DOCUMENTED_ONLY` | Exists as prose/config description; no implementation inspected |
| `CONFIGURED` | Config files present; not exercised |
| `IMPLEMENTED` | Source code present and read; not executed |
| `TESTED` | A test was actually run and passed (NOT achieved in this review) |
| `INTEGRATION_VERIFIED` | End-to-end runtime behaviour verified (NOT achieved) |
| `UNKNOWN` | Insufficient evidence |

**Nothing in this package is `TESTED` or `INTEGRATION_VERIFIED`.** Test files and CI
workflow definitions exist, but no test was executed and no CI run evidence for this
commit was retrieved.

---

## 1. Direct observations (what the files show)

### 1.1 Repository shape

- 312 files tracked at the pinned commit.
- Top-level areas: `AGENTS.md`, `agent-briefing.md`, `prioritization.md`, `prompts.md`,
  `learning_engine/`, `memory/`, `references/`, `runtime/`, `scripts/`, `skills/`,
  `.agents/`, `.opencode/`, `testing/`, `writeups/`, `wordlist/`, `.github/`.
- `skills/` contains 22 `*.md` skill files; `.agents/skills/<name>/SKILL.md` contains 22
  `SKILL.md` files whose contents are **byte-identical** to the corresponding `skills/*.md`
  files (verified by SHA-256 comparison). These are two copies of the same 22 playbooks,
  not 44 distinct skills.

### 1.2 Canonical agent registry

`runtime/registry.json` is the machine-readable registry. Its `agents` map contains
**six** entries:

| Agent id | Registered skills |
|----------|-------------------|
| `orchestrator` | `*` |
| `recon-agent` | recon, subdomain-enumeration, subdomain-takeover |
| `dorking-agent` | dorking |
| `js-agent` | api-testing |
| `fuzzing-agent` | api-testing, graphql |
| `understand-agent` | auth-bypass, jwt, oauth, business-logic |

The registry records skill assignments only; it does **not** define responsibilities in prose.

### 1.3 Two conflicting agent taxonomies

`runtime/opencode/agents/` contains **11** agent files, which fall into two inconsistent sets:

**Set A — matches `runtime/registry.json` (5 collection agents):**
`recon-agent.md`, `dorking-agent.md`, `js-agent.md`, `fuzzing-agent.md`,
`understand-agent.md`. These describe collection-only roles (no exploitation).

**Set B — front-matter agents not present in `registry.json`:**
`orchestrator.md`, `hunter.md`, `recon.md`, `librarian.md`, `reporter.md`, `validator.md`.
These use YAML front matter (`id`, `name`, `skills`) and describe a different division of
labour (orchestrator plans; hunter exploits; validator verifies; reporter writes; librarian
maintains the learning corpus).

**Direct contradiction:**

- `runtime/opencode/ORCHESTRATION.md` and `AGENTS.md` describe the **orchestrator as the
  attacker** that does “ALL exploitation and validation”, with the five collection agents
  feeding it.
- `runtime/opencode/agents/orchestrator.md` states the opposite: *“Plans and supervises
  hunts. Never performs testing itself.”*

Both are `DOCUMENTED_ONLY`. Neither is authoritative over the other in the repository.
**Resolution status: UNRESOLVED.** This is an internal inconsistency in the upstream
project, not a defect introduced by this package.

### 1.4 How the agent model should be described

Safe statement: the repository documents a **multi-agent design** with a canonical registry
of **one coordinator plus five collection sub-agents**, and separately contains an
alternative set of agent briefs (hunter/validator/reporter/librarian) that are **not**
registered. The intended effective architecture cannot be determined from static files
alone.

`INFERENCE`: the registry plus `ORCHESTRATION.md` is more likely to be the live design,
because the registry is machine-readable and referenced by `scripts/skill_registry.py`.
This is an inference, not a verified fact.

### 1.5 Skills

- 22 skill playbooks exist, duplicated in `skills/` and `.agents/skills/`.
- Topics: api-testing, auth-bypass, business-logic, csrf, dorking, file-upload, graphql,
  idor, jwt, learning-engine-integration, lfi, master-bugbounty-rules, oauth,
  open-redirect, race-condition, recon, sqli, ssrf, ssti, subdomain-enumeration,
  subdomain-takeover, xss.
- `references/skill-router.md`, `runtime/registry.json`, and `scripts/skill_registry.py`
  provide skill-routing material.
- Status: `DOCUMENTED_ONLY` for the playbooks; `IMPLEMENTED` for `scripts/skill_registry.py`
  (code present and read, not executed).

### 1.6 Learning engine — correction of earlier claims

The earlier draft described this as a "RAG" / "knowledge graph + retrieval" system. That
was **not supported** by the implementation. What the code actually contains:

| Module | Observed implementation | Status |
|--------|-------------------------|--------|
| `learning_engine/core/storage.py` | SQLite wrapper | `IMPLEMENTED` |
| `learning_engine/core/schema.py` | Tables: `meta`, `findings`, `triage`, `lessons`, `patterns`, `signals_meta`; FTS5 virtual tables `findings_fts`, `lessons_fts` | `IMPLEMENTED` |
| `learning_engine/retrieval/search.py` | **SQLite FTS5 full-text search with multi-token `LIKE` fallback** | `IMPLEMENTED` |
| `learning_engine/graph/builder.py` | Exports nodes/edges (`target`, `vuln_class`, `signal`, `lesson`) to JSON from SQLite rows | `IMPLEMENTED` |
| `learning_engine/scoring/engine.py` | Weighted signal scoring clamped to [0,1] | `IMPLEMENTED` |
| `learning_engine/analytics/patterns.py` | Aggregation helpers | `IMPLEMENTED` |
| `learning_engine/ingestion/*` | Finding/triage persistence | `IMPLEMENTED` |
| `learning_engine/engine.py` | Public API with five hooks | `IMPLEMENTED` |

**Corrected conclusions:**

- Retrieval is **lexical** (FTS5 + `LIKE`). There are **no embeddings, vector store,
  FAISS, Chroma, cosine similarity, or semantic search** anywhere in `learning_engine/`
  (grep for those terms returns nothing).
- The "knowledge graph" is a **JSON node/edge export** computed from SQLite rows, not a
  graph database and not a persisted graph structure.
- Therefore the earlier "RAG-based" characterisation is **withdrawn**. A correct label is:
  *SQLite-backed finding/lesson memory with lexical full-text retrieval and a JSON graph
  export.*

### 1.7 Memory system

- `memory/` contains: `CONTEXT_LEDGER.md`, `FALSE_POSITIVE_DB.md`, `methodology.md`,
  `patterns.md`, `report-lessons.md`, and `targets/{auth-bypass,idor,sqli,ssrf,xss}.md`.
- These are **Markdown templates/ledgers** maintained by agent procedure.
  `DOCUMENTED_ONLY` for the workflow; plain files on disk.

### 1.8 Runtime / harness configuration

- `.opencode.json` configures a `chrome-devtools` MCP server and browser capture settings.
  `CONFIGURED` (not exercised).
- `opencode.json` configures OpenCode agent tools/instructions. `CONFIGURED`.
- `package.json` declares Playwright dependencies and scripts. `CONFIGURED`.
- `.opencode/commands/` contains 8 command markdown files. `DOCUMENTED_ONLY`.
- `.github/workflows/engine.yml` and `.github/workflows/registry.yml` define CI jobs
  (pytest, registry check, preflight, offline pipeline smoke). `CONFIGURED`; no run
  evidence inspected.

### 1.9 Writeups

- `writeups/` contains `raw/`, `processed/`, `feeds/sample/`, `metadata/`, `index.md`.
- The included writeups are **sample/illustrative** files shipped with the repo, not a
  real corpus.
- Status: `DOCUMENTED_ONLY` for the ingestion workflow.

---

## 2. Architecture overview (descriptive, not prescriptive)

```
Repository root
├── AGENTS.md                master directives (prose)
├── agent-briefing.md        knowledge-state briefing (prose)
├── prioritization.md        P1–P4 framework (prose)
├── prompts.md               prompt library (prose)
├── runtime/
│   ├── registry.json        canonical agents + skills + routes (machine-readable)
│   ├── opencode/            orchestration manual + 11 agent briefs (two conflicting sets)
│   └── antigravity/         alternate harness docs
├── .agents/skills/          22 SKILL.md playbooks (duplicate of skills/)
├── skills/                  22 skill .md playbooks
├── learning_engine/         SQLite memory + FTS5 retrieval + JSON graph export + scoring
├── memory/                  markdown ledgers / FP DB / per-class notes
├── references/              config index, skill router, ownership/verification maps
├── scripts/                 skill registry, preflight, update pipeline, tests
├── .opencode/ + .opencode.json + opencode.json   harness + MCP config
├── .github/workflows/       CI definitions
├── writeups/                sample raw/processed writeups
└── testing/                 real target evidence  (EXCLUDED from package snapshot)
```

---

## 3. Implementation maturity summary

| Area | Status | Evidence |
|------|--------|----------|
| Agent roles / workflows | `DOCUMENTED_ONLY` | Prose in `ORCHESTRATION.md` + agent briefs; contradictory |
| Agent registry | `IMPLEMENTED` (data) | `runtime/registry.json` parsed; 6 agents |
| Skill playbooks | `DOCUMENTED_ONLY` | 22 markdown files, duplicated |
| Skill registry script | `IMPLEMENTED` | `scripts/skill_registry.py` read; not run |
| Runtime preflight script | `IMPLEMENTED` | `scripts/runtime_preflight.py` read; not run |
| Learning engine core | `IMPLEMENTED` | Python modules read; not run |
| Retrieval | `IMPLEMENTED` (lexical FTS5) | `retrieval/search.py`; no embeddings |
| Graph export | `IMPLEMENTED` (JSON export) | `graph/builder.py` |
| Scoring | `IMPLEMENTED` | `scoring/engine.py` |
| Memory ledgers | `DOCUMENTED_ONLY` | Markdown files |
| OpenCode / MCP config | `CONFIGURED` | config files present |
| Playwright automation | `CONFIGURED` | `package.json` |
| CI workflows | `CONFIGURED` | YAML present; no run evidence |
| Tests | `TEST FILES EXIST` | `scripts/test_*.py`; **not executed** |
| Integration | `UNKNOWN` | No runtime verification |

---

## 4. Observed design elements (documented, not verified as effective)

The documentation describes: scope restriction, on-demand skill loading, false-positive
gates, evidence requirements, specialised sub-agents, persistent target workspaces,
prioritisation, exploit/impact validation, historical-context retrieval, writeup ingestion,
agent briefing/commands, and browser/MCP integration.

These are recorded as **documented design intent**. Their effectiveness is untested here.

---

## 5. Limitations of this review

1. Static inspection only; **no execution** of scripts, engine, or agents.
2. **No tests run** and no CI run evidence for this commit.
3. Agent architecture is **internally contradictory**; effective design unknown.
4. `prompts.md` (120 KB) and `prioritization.md` only partially read.
5. Skill playbook bodies enumerated and spot-checked, not exhaustively reviewed.
6. Third-party licensing of embedded content unknown.
7. `.git` history excluded from the snapshot; no contributor history analysed.
8. `testing/` excluded — real-target evidence was not reviewed for architecture relevance.

---

## 6. Research observations (NOT adoption recommendations)

The following are neutral observations that the external architect may weigh. They do not
constitute an adoption decision, and no CBH change is implied.

1. A machine-readable agent/skill registry exists, which is a concrete pattern for routing.
2. Retrieval is simple lexical full-text, not semantic; this has different capability and
   cost characteristics than embedding-based retrieval.
3. The repository contains competing agent descriptions and a self-contradictory
   orchestrator role — a caution about treating documentation as a specification.
4. Tests and CI definitions exist but were not verified to pass.

---

*Source: https://github.com/0xmannaf/Ai-Hunting @ 3c1e9a021779eeffbd2c021b8664aa24c1df04b2*
