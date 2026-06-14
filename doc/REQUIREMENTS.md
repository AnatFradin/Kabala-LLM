# Kabala-LLM — Requirements

## 1. Vision

A central, team-accessible "LLM Wiki" for our Kabbalah study materials — following the
**Karpathy "LLM wiki" pattern**:

- **Raw materials are immutable** (source lessons, transcripts, PDFs, docs — e.g. the
  existing Google Drive folder `My Drive/Кабала`).
- An **LLM ingestion pipeline** processes raw materials into structured, linked wiki
  pages (Zettelkasten-style notes), similar to the existing `ingest` / `enrich-graph` /
  `lint` / `lint-graph` skills already used locally.
- The generated wiki is **human-readable and browsable** — not hidden inside a vector
  DB. Content should remain compatible with Obsidian (markdown + `[[wikilinks]]` +
  graph view).
- On top of this wiki, a **chat interface** lets team members ask questions, with the
  LLM grounded in the actual wiki pages (full-page context, not opaque embeddings —
  though a lightweight search/index layer to *find* relevant pages first is fine).

## 2. Users & Roles

- **Team members** — currently a small group (you + collaborators), accessible to
  people in different countries.
- **Roles** (introduced progressively):
  - `admin` — manage content, users, ingestion, settings
  - `reader` — browse wiki + chat
  - (future) per-user workspace / personal notes layer
- **Phase 1**: simple login is enough; full role separation can start minimal
  (e.g. just admin vs reader) and expand later.
- **Future**: separate workspace per user/login (their own notes/annotations on top of
  the shared wiki).

## 3. Core Functional Requirements

### Phase 1 — MVP (chat-first)
- [ ] Chat interface where team members ask questions about the learning materials.
- [ ] LLM answers grounded in the existing wiki content (full-page retrieval, not pure
      vector RAG).
- [ ] Basic authentication (who can access the chat at all).
- [ ] Deployed somewhere accessible online (not just local).

### Phase 2 — Wiki browsing
- [ ] Web UI to browse the wiki content itself (read-only), mirroring the
      Obsidian/Zettelkasten structure (linked notes, graph-style navigation).
- [ ] Admin/reader role separation.
- [ ] Content remains immutable/raw + generated wiki separation, consistent with
      existing `ingest`/`lint` workflow.

### Phase 3 — Content management
- [ ] Admin can trigger/manage ingestion of new raw materials via the UI (not just
      local CLI skills).
- [ ] Content versioning / audit trail (since raw is immutable, wiki pages may be
      regenerated — track history).
- [ ] **Automated ingestion from links**:
  - [ ] Admin submits a Google Drive document link → pipeline fetches the source
        document, stores it as immutable raw material, and generates a corresponding
        wiki page/note.
  - [ ] Admin submits a YouTube link for the **weekly lesson** → pipeline fetches
        the video (transcript/audio), stores it as immutable raw material, and
        generates a new lesson wiki page.
  - [ ] Each generated lesson/note file is **linked back to its original source
        material** (Zettelkasten-style reference/backlink to the source Drive doc
        or YouTube video), and linked into the broader wiki graph (related topics,
        prior lessons, etc.) via `enrich-graph`-style processing.
  - [ ] **Reuse existing asset**: an existing Python script
        (`/Users/anatfradin/convert-google-doc-md/gdoc-to-raw.py`, used via the local
        `/gdoc-lesson` command) already converts a Google Doc URL into a clean raw
        markdown file. This logic should be ported/adapted into the automated
        cloud pipeline rather than rebuilt from scratch.
  - [ ] **New capability needed**: YouTube → raw markdown conversion (fetch
        transcript/audio, produce a raw lesson file) does not exist yet and needs to
        be built as part of this pipeline.

### Phase 4 — Personalization
- [ ] Per-user workspace: personal notes, bookmarks, or annotations layered on top of
      the shared wiki.
- [ ] Possibly per-user chat history.

## 4. Non-Functional Requirements

- **Accessibility**: usable by team members in different countries (latency,
  availability).
- **Single integrated portal (KEY UX)**: the end-user experience must be **one web URL**
  where a non-technical person can both **browse all the learning materials** AND
  **chat/ask about them** — together, in one place. No local apps or technical setup
  required to *use* the system.
- **Non-technical end users**: most team members are not technical. Local Obsidian is
  therefore an **authoring/power-user tool only** (for admins/editors), NOT the
  end-user interface. Browsing the wiki must be elevated to a core part of the product,
  not a Phase-2 afterthought.
- **Cost**: symbolic/low cost acceptable; prioritize low-maintenance, low-cost hosting
  for MVP, but architecture should allow scaling later.
- **Methodology**: Agile — ship a usable MVP first (Phase 1 chat), iterate in small
  increments. Each phase above should be independently shippable.
- **Data integrity**: raw source materials are never modified by the pipeline — only
  read and processed into derived wiki content.
- **Compatibility**: generated wiki content should remain valid Obsidian vault content
  (so it can also be browsed locally in Obsidian, independent of the web app).

## 5. Open Questions (to resolve in Architecture phase)

- Hosting platform: evaluate AWS vs. simpler alternatives (Vercel/Render/Fly.io +
  managed Postgres, etc.) for cost/complexity vs. global accessibility.
- LLM provider/model choice and cost model for chat (per-query cost at small team
  scale).
- How ingestion pipeline (currently local skills) moves into an automated,
  cloud-triggered process.
- Search/index layer for finding relevant wiki pages before feeding to LLM (keyword
  search vs. lightweight embeddings vs. metadata/graph-based lookup).
- Auth provider choice (e.g. simple email/password vs. OAuth/Google login — useful
  since source content already lives in Google Drive).

## 6. Source Content & Existing Assets

- Existing raw materials: Google Drive — `My Drive/Кабала` (mixed `.md`, `.pdf`,
  `.docx`, `.pptx`, images, etc.), Russian/Hebrew content on Kabbalah lessons,
  holidays, articles, etc.
- Existing local Obsidian vault (`Личные мысли/Личные записи`) already implements the
  `raw/` (immutable) → `wiki/` (generated, linked, Zettelkasten) pattern, with:
  - `raw/` organized by topic (e.g. `50-Кабала/`)
  - `wiki/index.md`, `wiki/log.md`, `wiki/overview.md`, `wiki/Глоссарий.md`,
    `wiki/concepts/`, `wiki/analyses/`, `wiki/sources/`
  - A `CLAUDE.md` operating manual defining the ingest/lint/enrich-graph workflow,
    page format (YAML frontmatter + `[[wikilinks]]`), and citation rules.
- Existing local workflow (skills): `ingest`, `enrich-graph`, `lint`, `lint-graph`,
  `kabbala-gdoc-lesson`/`gdoc-lesson`, `update-wiki` — these establish the raw → wiki
  pipeline pattern this project should build on/automate.
- Existing reusable tool: `/Users/anatfradin/convert-google-doc-md/gdoc-to-raw.py`
  (Python, with `credentials.json` + cached OAuth token) — converts a Google Doc URL
  into a raw markdown file. To be ported into the cloud ingestion pipeline (Phase 3).
