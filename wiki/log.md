# Activity Log — Kabala Wiki

Append-only. Newest entries at the bottom.

---

## 2026-06-20 — Initial wiki setup + Sefirot ingest

**Setup**
- Installed operating manual `CLAUDE.md` (adapted to repo-relative paths).
- Created wiki skeleton: `index.md`, `overview.md`, `glossary.md`, `log.md`, and `concepts/`.

**Ingested cluster: Сфирот** (from `raw/50-Кабала/`)
- Sources read: `Кетер.md`, `Хохма.md`, `Бина.md`, `Хесед.md`, `Гвура.md`, `Тиферет.md`, `Нецах.md`, `Ход.md`, `Йесод.md`, `Малкут.md`, `Древо Жизни + Парцуфим.md`.
- Created concept pages: [[Кетер — Венец]], [[Хохма — Мудрость]], [[Бина — Понимание]], [[Хесед — Милосердие]], [[Гвура — Суд]], [[Тиферет — Гармония]], [[Нецах — Вечность]], [[Ход — Слава]], [[Йесод — Основание]], [[Малхут — Царство]].
- Created MOC: [[10 Сфирот — Древо Жизни]].
- Updated `index.md`, `overview.md`, `glossary.md`.

**Coverage so far:** 11 raw files processed → 11 wiki pages (10 concepts + 1 MOC).

**Still in queue (raw/50-Кабала/):** root concept files (Заповедь, Тикун, тело желания, правая/левая/чистая линия, Верхние/Нижние Сефирот, Авраам/Нимрод/Мордехай/Пурим, Малхут-аспект), `Hebrew/`, `уроки с Леей/` (~110 files), `уроки с Леей/Тора/` (weekly portions), images. Next batch: remaining root concept files of `50-Кабала/`.

---

## 2026-06-20 — Ingest batch 2: tree structure

**Processed** (raw/50-Кабала/ root → consolidated concept pages):
- [[Мухин и Мидот — Верхние и Нижние Сефирот]] ← `Верхние Сефирот - ספירות מוכין.md` + `Нижние Сефирот - **ספירות המидות**.md`
- [[Три линии — Колонны Древа]] ← `правая линия…` + `левая линия…` + `чистая линия…`
- [[Малхут — Царство]] updated ← `Малхут - желание насладиться ради себя.md` (aspect folded in)

**Skipped (empty / no content):** `тело желания.md`, `Тикун - תיקון.md`, `Заповедь.md` — will ingest once filled.

**Coverage so far:** ~18 raw sources processed → 13 concept/MOC pages (+ skeleton); 3 empty files skipped.

**Still in queue (raw/50-Кабала/ root):** `"Союз соли"…`, `Авраам - как венец…`, `Авраам - это Хесед`, `Кабала Урок 25 окт 2023` (→ sources/), `Мордехай`, `Нимрод`, `Пурим…`, `праздники`. Then `Hebrew/`, `уроки с Леей/` (~110), `Тора/`.
