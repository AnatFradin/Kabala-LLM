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

---

## 2026-06-20 — Ingest batch 3: figures, lesson — `50-Кабала/` root complete

**Processed:**
- [[Авраам — Хесед]] ← `Авраам - как венец духовного развития через родословную.md` + `Авраам - это Хесед.md`
- [[Союз соли — Остаток осознания]] ← `"Союз соли" - Урок выучен…md`
- [[Кабала Урок 25 окт 2023]] — first `sources/` page ← `Кабала Урок 25 окт 2023.md`
- Bidirectional link added: [[Хесед — Милосердие]] ↔ [[Авраам — Хесед]]

**Skipped (empty):** `Нимрод.md`, `Мордехай.md`, `Пурим - …**.md`, `праздники.md`.

**`raw/50-Кабала/` root: ✅ COMPLETE** — all 28 root `.md` files handled (21 → pages, 7 empty skipped).

**Next:** `raw/50-Кабала/Hebrew/` (6 files), then `уроки с Леей/` (~110) + `Тора/`.

---

## 2026-06-20 — Ingest batch 4: `Hebrew/` folder complete

**Processed:**
- [[Подобие свойств — Любовь]] ← `אהבה = השתוות הצורה.md` + `קבלה לעם.md`
- [[Корни и ветви — Причина и следствие]] ← `שורשים וענפים - סיבה ותוצאה.md`
- [[Талмуд Десяти Сфирот — ТЭС]] ← `תלמוד 10 הספירות.md`
- MOC enriched (правая=мужская, левая=женская) ← `עץ החיים - Дерево Жизни - 10 Сфирот.md` (already cited by MOC)

**Skipped (empty):** `פירוש מילים (שורשים) בתלמוד 10 ספירות כרך א.md`.

**`raw/50-Кабала/Hebrew/`: ✅ COMPLETE** — 6 files (5 → pages/MOC, 1 empty skipped).

**Next (the big one):** `raw/50-Кабала/уроки с Леей/` (~110 files) + `Тора/`.
