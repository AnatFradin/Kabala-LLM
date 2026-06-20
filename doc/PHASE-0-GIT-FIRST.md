# Phase 0 — Centralized OKF Wiki on GitHub

Status: **Decided approach.** One private GitHub repo holds all our Kabbalah materials as
an **OKF-format wiki**; every member uses it as the grounding source for their own AI
(Claude / ChatGPT); predefined **skills** add new documents in OKF format. No hosting,
low cost. The same repo becomes the source of truth if we later graduate to a hosted
portal (see [ARCHITECTURE.md](ARCHITECTURE.md) / [PLATFORM-COMPARISON.md](PLATFORM-COMPARISON.md)).

## The decision — 4 pillars

1. **One centralized GitHub repo** (private) — holds `raw/` (immutable sources) + `wiki/`
   (generated knowledge). Shared with the team.
2. **Managed as an OKF wiki** — `wiki/` follows the Open Knowledge Format: markdown + YAML
   frontmatter, one concept per file, standard markdown links, citations to sources.
3. **User prompts for Claude & ChatGPT** — ready-made prompts that point each member's AI
   at the repo as its grounding source for learning/investigation (grounded + cited).
4. **Skills to add documents** — predefined slash-commands that turn a new source into an
   OKF wiki page and commit it.

## Progress snapshot — 2026-06-20

**Done ✅** (all in remote: [AnatFradin/Kabala-LLM](https://github.com/AnatFradin/Kabala-LLM), in sync)
- Private repo created & pushed.
- `raw/` seeded — **163 files (140 markdown)** under `50-Кабала/`, immutable.
- `wiki/` skeleton: `index`, `overview`, `glossary`, `log`.
- First OKF ingest — **sefirot cluster**: 11 wiki pages (10 concepts + MOC).
- Operating manual `CLAUDE.md`; conventions: raw immutable, `log.md` changelog.

**Remaining 🚧 / Next ⬜**
- **Ingest the rest into OKF**: ~140 raw markdown sources → wiki pages (~11 done). *Batches.*
- **OKF conformance pass**: retrofit the 11 existing pages to **dual links** (wikilink +
  markdown link); confirm reserved-file structure. (frontmatter `type` already ✓)
- **User prompts** (Claude + ChatGPT) in `prompts/`.
- **Skills** in `.claude/commands/` that emit OKF pages.
- **README** + invite the 11.

---

## 1 · Centralized repo
- Private repo `AnatFradin/Kabala-LLM`; invite the 11 — Read for readers, Write for maintainers.
- `raw/` = immutable source of truth (never edited — `CLAUDE.md` rule).
- `wiki/` = generated OKF knowledge. Reserved files: `wiki/index.md`, `wiki/log.md`.

## 2 · OKF wiki format
Per OKF v0.1 (Google Cloud), each `wiki/` page is:
- markdown + YAML frontmatter; **required** `type`; recommended `title`, `description`,
  `resource`, `tags`, `timestamp`;
- one concept per file (concept id = file path); relationships via **standard markdown
  links** (render on GitHub, agent-friendly);
- a **citation** = a link from the page to the source supporting a claim (our `📂 Raw:` link).

> **Link style — dual links.** Every cross-link is written as the Obsidian `[[wikilink]]`
> immediately followed by a standard markdown link `[text](<path>)`, one after another.
> This keeps the Obsidian graph working **and** renders on GitHub / satisfies OKF. The 11
> existing pages are being retrofitted to this dual-link format.

## 3 · User prompts (Claude & ChatGPT)
Two ready-made prompts (stored in `prompts/`) so any member can ground their AI on the repo:
- **Claude** — connect the repo (Projects → GitHub connector, or Claude Code locally).
- **ChatGPT** — connect via GitHub connector (Plus+), or a shared Custom GPT / uploaded
  bundle (works on free).

Both encode the `CLAUDE.md` answering rules: answer **only** from `wiki/`, **cite the
source page**, handle Russian/Hebrew, and say "not in the materials" when unknown — so
every member's AI behaves consistently. Refresh = connector **Sync** or `git pull`.

## 4 · Skills to add documents (OKF)
Predefined slash-commands (in `.claude/commands/`, documented in `CLAUDE.md`) the
maintainer runs:
- `/gdoc-lesson` — Google Doc URL → `raw/` markdown → ingest.
- `/ingest` — new/changed `raw/` → OKF wiki page(s) + update `index`/`log`.
- `/enrich-graph`, `/lint`, `/lint-graph` — strengthen links, quality checks.

All skills emit **OKF-compliant** pages.

## Maintainer workflow
New source → `/gdoc-lesson` (or drop a file in `raw/`) → `/ingest` (produces the OKF page)
→ review → commit & push. Members then refresh their AI (connector **Sync** / `git pull`).

---

## Next steps (checklist)
- [ ] Ingest remaining `raw/50-Кабала/` into OKF wiki pages (batches)
- [ ] OKF conformance pass on the 11 existing pages (retrofit to dual links)
- [ ] Write Claude + ChatGPT user prompts (`prompts/`)
- [ ] Add `.claude/commands/` skill files (OKF-emitting)
- [ ] `README.md` + privacy/usage note
- [ ] Invite the 11 collaborators
- [ ] *(optional)* Quartz / GitHub Pages for nicer browsing

## Later — graduation
If Phase 0 proves useful (regular use; the only pain is manual refresh or the lack of a
single URL), graduate to a hosted portal — reusing this repo as the source of truth.
