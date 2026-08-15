# 📚 Wiki Creation Project

> A simple, repeatable system for keeping project documentation alive — using a `docs/` folder as your source of truth and a `wiki/` folder of AI-generated summaries derived from it.

---

## 🧠 The Big Idea (Read This First)

Most projects die from bad docs. Either:
- Nobody writes them.
- Someone writes them once and they rot.
- They live in 5 different places and nobody agrees which one is right.

This system fixes that with **two simple rules**:

```
Rule 1: Humans write docs/ — always authoritative, always up to date.
Rule 2: AI writes wiki/ — always derived from docs/, never edited by hand.
```

That's it. Everything else in this repo supports those two rules.

---

## 🗂️ Folder Structure — What Goes Where

```
your-project/
│
├── docs/                          ← YOU write here. This is the truth.
│   ├── domain/                    ← What the product/business does (concepts, rules)
│   ├── tech-design/               ← How it's built (architecture, APIs, schemas)
│   └── project-management/        ← Why decisions were made (PRDs, roadmaps, plans)
│
├── wiki/                          ← AI writes here. Never edit manually.
│   ├── domain/
│   │   └── overview.md            ← Summary of domain concepts
│   ├── tech-design/
│   │   ├── backend/
│   │   │   └── overview.md        ← Backend architecture summary
│   │   ├── frontend/
│   │   │   └── overview.md        ← Frontend architecture summary
│   │   └── data-modelling/
│   │       └── overview.md        ← Data models and schemas summary
│   ├── project-management/
│   │   └── overview.md            ← PRD/roadmap/stakeholder summary
│   ├── index.md                   ← Master list of all wiki pages
│   ├── log.md                     ← Append-only history of every wiki update
│   ├── decisions.md               ← Architectural Decision Records (ADRs)
│   └── glossary.md                ← Every term/acronym defined in one place
│
└── AGENTS.md                      ← Instructions for AI agents on how to use this system
```

**One sentence per folder:**
- `docs/` = the original writing. Treat it like code — review it, version it, own it.
- `wiki/` = the readable summary. Fast to scan, always current, generated not written.
- `AGENTS.md` = the rulebook that tells any AI (Kiro, Claude, Copilot) what to do when a doc changes.

---

## 🚀 Setup Guide

### Option A — Brand New Project

Follow these steps **in order**. Don't skip.

---

#### Step 1: Create the folder structure

```bash
mkdir -p docs/domain
mkdir -p docs/tech-design
mkdir -p docs/project-management
mkdir -p wiki/domain
mkdir -p wiki/tech-design/backend
mkdir -p wiki/tech-design/frontend
mkdir -p wiki/tech-design/data-modelling
mkdir -p wiki/project-management
```

On Windows (PowerShell):
```powershell
New-Item -ItemType Directory -Force -Path docs/domain, docs/tech-design, docs/project-management
New-Item -ItemType Directory -Force -Path wiki/domain, wiki/tech-design/backend, wiki/tech-design/frontend, wiki/tech-design/data-modelling, wiki/project-management
```

> Why these folders? Because every project has three types of knowledge:
> - **Domain** — what the business does and why
> - **Tech Design** — how the system is built
> - **Project Management** — what was planned, decided, and shipped

---

#### Step 2: Create the four core wiki files

These are the backbone. Create them empty — they'll fill up over time.

**`wiki/index.md`** — the home page of your wiki
```markdown
# Wiki Index

> **Last ingested:** YYYY-MM-DD

| Page | Purpose |
|------|---------|
| [domain/overview.md](domain/overview.md) | Domain concepts |
| [tech-design/backend/overview.md](tech-design/backend/overview.md) | Backend architecture |
| [decisions.md](decisions.md) | Architectural decisions |
| [glossary.md](glossary.md) | Term definitions |
| [log.md](log.md) | Ingest history |
```

**`wiki/log.md`** — append-only history, one line per wiki update
```markdown
# Wiki Ingest Log

Format: [YYYY-MM-DD] UPDATE wiki/<page>.md — source: docs/<file> — <summary>

<!-- entries go below -->
```

**`wiki/decisions.md`** — for every "why did we build it this way?" moment
```markdown
# Architectural Decision Records (ADRs)

## ADR-0001: <Title>
**Date:** YYYY-MM-DD
**Status:** Accepted

### Context
What problem were we solving?

### Decision
What did we decide?

### Consequences
What are the tradeoffs?
```

**`wiki/glossary.md`** — one place for every term, acronym, and jargon word
```markdown
# Glossary

| Term | Definition |
|------|-----------|
| Example | What it means |
```

---

#### Step 3: Create AGENTS.md

This file tells any AI assistant exactly how to behave with your docs. Copy the template from this repo's `AGENTS.md` and customize the **Source → Wiki Mapping** table to match your project's actual doc files.

The critical section is this table — update it whenever you add a new source doc:

```markdown
| Source doc (docs/)              | Feeds wiki page(s)                              |
|---------------------------------|-------------------------------------------------|
| docs/domain/**                  | wiki/domain/overview.md                         |
| docs/tech-design/backend/**     | wiki/tech-design/backend/overview.md            |
| docs/project-management/**      | wiki/project-management/overview.md             |
| Any doc with new terms          | wiki/glossary.md                                |
| Any doc with design tradeoffs   | wiki/decisions.md                               |
```

---

#### Step 4: Add your first source doc

Drop a real document into the right `docs/` subfolder. Examples:
- A PRD → `docs/project-management/PRD-my-product.md`
- An API spec → `docs/tech-design/api-spec.md`
- Domain rules → `docs/domain/business-rules.md`

Write it in plain Markdown. Be thorough — this is the truth.

---

#### Step 5: Generate the first wiki pages

Hand the source doc to your AI assistant (Kiro, Claude, etc.) and say:

> "Follow the ingest rule in AGENTS.md. The source doc is docs/project-management/PRD-my-product.md. Generate the matching wiki pages, update the log and index."

The AI will:
1. Read the source doc in full
2. Check which wiki pages it maps to (from the table in AGENTS.md)
3. Generate or update only those wiki pages
4. Append a line to `wiki/log.md`
5. Update the `Last ingested` date in `wiki/index.md`

---

#### Step 6: Commit everything

```bash
git add .
git commit -m "docs: initial wiki scaffold + first ingest"
git push
```

Done. Your wiki is live.

---

### Option B — Existing Project (Adding Wiki to a Project That Already Has Docs)

If you already have documentation scattered around, here's how to migrate without breaking anything.

---

#### Step 1: Audit what you already have

List your existing docs:
```bash
# Find all markdown files in your project
find . -name "*.md" -not -path "./.git/*"
```

Group them mentally into three buckets:
- **Domain knowledge** → goes in `docs/domain/`
- **Technical design** → goes in `docs/tech-design/`
- **Project management** → goes in `docs/project-management/`

---

#### Step 2: Create the wiki folder structure

Same as Option A Step 1. Run the folder creation commands above.

---

#### Step 3: Move (or copy) existing docs into docs/

```bash
# Example: move an existing PRD
mv existing-prd.md docs/project-management/PRD.md

# Example: move architecture docs
mv architecture.md docs/tech-design/architecture.md
```

> ⚠️ If your existing docs live elsewhere and other tools reference them, **copy** instead of move. Update references later.

---

#### Step 4: Create AGENTS.md

Same as Option A Step 3. Fill in the mapping table to reflect your actual existing files.

---

#### Step 5: Create the four core wiki files

Same as Option A Step 2.

---

#### Step 6: Run a full first-pass ingest

Tell your AI assistant:

> "Do a full first-pass ingest. Read all files under docs/, check the mapping table in AGENTS.md, and generate wiki pages for each. Update wiki/log.md and wiki/index.md when done."

This generates your entire wiki from scratch in one shot.

---

#### Step 7: Review, then commit

Skim the generated wiki pages. They should accurately reflect your docs. If something looks wrong, fix the **source doc** in `docs/`, then re-run ingest for that file — never edit the wiki directly.

```bash
git add .
git commit -m "docs: add wiki system + initial ingest from existing docs"
git push
```

---

## 🔄 Day-to-Day Workflow (Once Set Up)

This is what you do every time docs change:

```
You update a doc in docs/
        ↓
Tell AI: "Re-ingest docs/X.md following AGENTS.md rules"
        ↓
AI reads source doc → updates wiki page(s) → appends log → updates index date
        ↓
You review the wiki diff → commit
```

That's the whole loop. **You never write wiki pages by hand.**

---

## 📋 The Ingest Rule (What the AI Does Every Time)

When any file in `docs/` changes, the AI must follow these steps in order:

```
1. Read the full updated source doc
2. Check the mapping table in AGENTS.md — find which wiki page(s) it feeds
3. Read the current content of those wiki pages
4. Update ONLY the affected sections — don't rewrite unrelated content
5. Append one line to wiki/log.md:
   [YYYY-MM-DD] UPDATE wiki/<page>.md — source: docs/<file> — <brief summary>
6. Update the "Last ingested" date in wiki/index.md
7. Cross-link related pages using relative paths
```

This rule lives in `AGENTS.md`. The AI reads it automatically when working in this repo.

---

## 📄 File Reference — What Each File Is For

### `wiki/index.md`
The front door. Anyone new to the project starts here. Lists every wiki page with a one-line description. Has a "Last ingested" date at the top so you instantly know if it's stale.

### `wiki/log.md`
The receipt trail. Every single wiki update gets one line here. Append-only — never delete entries. Lets you audit exactly what changed, when, and from which source.

### `wiki/decisions.md`
The "why" file. When you make a non-obvious architectural or product decision, it goes here as an ADR. Format: context → decision → consequences. Invaluable for onboarding and for future-you wondering why something was built a certain way.

### `wiki/glossary.md`
One source for every term. Domain jargon, acronyms, product-specific words — all defined here. When a new doc introduces a term, the AI adds it here during ingest.

### `AGENTS.md`
The instruction manual for AI assistants. Contains:
- The source → wiki mapping table
- The ingest rule (step by step)
- Wiki page structure guidelines
- What NOT to do

---

## ✅ Rules to Live By

| ✅ Do This | ❌ Never Do This |
|-----------|----------------|
| Write source docs in `docs/` | Edit `wiki/` files directly as primary source |
| Let AI generate wiki pages | Manually write wiki summaries |
| Append to `wiki/log.md` on every update | Delete or edit log entries |
| Update the mapping table when adding new docs | Add docs to `docs/` without updating AGENTS.md |
| Fix errors in the source doc, then re-ingest | Fix errors directly in wiki pages |
| Keep wiki pages under ~300 lines | Let wiki pages grow into giant monoliths |

---

## 🧩 Real Example — How This Repo Works

This repo contains a real working example using a VWO PRD:

1. **Source doc:** `docs/project-management/PRD-VWO-com.md`
   - A full Product Requirements Document for VWO (Visual Website Optimizer)
   - Written once, authoritative

2. **Generated wiki page:** `wiki/project-management/overview.md`
   - Audience-structured summary: objectives, stakeholders, requirements table, KPIs, risks
   - Generated from the PRD, not written by hand

3. **Glossary updated:** `wiki/glossary.md`
   - 10 terms added from the PRD: CRO, DXO, SmartStats, A/B Test, GDPR, CCPA, etc.

4. **Log entry added:** `wiki/log.md`
   - `[2026-08-15] UPDATE wiki/project-management/overview.md — source: docs/project-management/PRD-VWO-com.md`

This is exactly what happens every time you feed a new doc into the system.

---

## ❓ FAQ

**Q: What if I want to add something to a wiki page that isn't in any source doc?**
A: Add it to the source doc first. Then re-ingest. The wiki is always downstream of docs.

**Q: Can I have multiple source docs feed the same wiki page?**
A: Yes. Update the mapping table in AGENTS.md to reflect that. The AI will merge content from all source docs into the one wiki page.

**Q: What if a wiki page gets too long?**
A: Split it. For example, `wiki/tech-design/backend/overview.md` can become separate pages for `auth.md`, `caching.md`, `query-engine.md`. Update the index and cross-links accordingly.

**Q: Do I need a specific AI tool to use this?**
A: No. Works with Kiro, Claude, GitHub Copilot, or any AI that can read files. The instructions are in plain English in AGENTS.md.

**Q: What if my team doesn't use AI tools?**
A: The `docs/` folder still works as a plain documentation system. The wiki just won't auto-generate — you'd have to write it manually (but then what's the point, right).

**Q: Can I add more folder categories under docs/?**
A: Yes. Just add a row to the mapping table in AGENTS.md and create the matching wiki subfolder.

---

## 🔗 Related Files

- [`AGENTS.md`](AGENTS.md) — AI agent instructions, mapping table, ingest rule
- [`wiki/index.md`](wiki/index.md) — wiki home page
- [`wiki/log.md`](wiki/log.md) — ingest history
- [`wiki/decisions.md`](wiki/decisions.md) — architectural decision records
- [`wiki/glossary.md`](wiki/glossary.md) — term definitions
- [`docs/project-management/PRD-VWO-com.md`](docs/project-management/PRD-VWO-com.md) — example source doc

---

*Built with the principle that good documentation systems should require as little willpower as possible.*
