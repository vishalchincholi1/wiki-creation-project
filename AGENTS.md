# AI Agent Instructions

This file governs how AI agents (Kiro, Claude, Copilot, etc.) should interact with this repository's documentation system.

---

## Source of Truth

All authoritative documentation lives in `docs/`. Wiki pages in `wiki/` are **derived** from those docs and must never be treated as primary sources.

```
docs/
  domain/               ← domain concepts, bounded contexts, business rules
  tech-design/          ← specs, architecture docs, API contracts
  project-management/   ← milestones, decisions, team context
wiki/                   ← AI-generated summaries (do not edit directly)
```

---

## Source → Wiki Mapping

| Source doc (docs/) | Feeds wiki page(s) |
|---|---|
| `docs/domain/**` | `wiki/domain/overview.md` |
| `docs/tech-design/backend/**` | `wiki/tech-design/backend/overview.md` |
| `docs/tech-design/frontend/**` | `wiki/tech-design/frontend/overview.md` |
| `docs/tech-design/data-modelling/**` | `wiki/tech-design/data-modelling/overview.md` |
| `docs/project-management/**` | `wiki/project-management/overview.md` |
| Any doc introducing new terms | `wiki/glossary.md` |
| Any doc capturing a design choice or tradeoff | `wiki/decisions.md` |

When a source doc changes, only update the wiki pages listed in the row(s) that match.

---

## Ingest Rule

When any file under `docs/` is created or updated, follow these steps in order:

1. **Read** the full updated source doc.
2. **Identify** which wiki page(s) it maps to (see table above).
3. **Read** the current content of each matched wiki page.
4. **Update** only the section(s) affected — do not rewrite unrelated content.
5. **Append** one line to `wiki/log.md`:
   ```
   [YYYY-MM-DD] UPDATE wiki/<page>.md — source: docs/<file> — <brief summary>
   ```
6. **Update** the `Last ingested` date at the top of `wiki/index.md`.
7. **Cross-link** pages using relative paths where relevant.

---

## Wiki Page Structure Guidelines

- Structure pages by **audience need**, not by source doc structure.
- Split large topics into focused pages (e.g. auth, caching, query engine as separate files — not one giant page).
- Keep each page under ~300 lines. If it grows beyond that, split it.
- Use relative links between wiki pages: `[glossary](../glossary.md)`.

---

## What NOT to Do

- Do not edit `wiki/` files as a primary source — always regenerate from `docs/`.
- Do not commit changes to `wiki/` without a corresponding `wiki/log.md` entry.
- Do not rename or move `docs/` files without updating the mapping table above.
