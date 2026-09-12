Independently verify that newly added or changed files in this repo (`raw/` and `wiki/`) contain no sensitive or private information, before they are pushed to this **public** repository.

## When to run

- **Automatically**, as the final step of `/kabbala-gdoc-lesson`, right after ingest and before asking the user to confirm the push — a finding here is a hard stop, not a warning.
- **On demand**, any time: `/kabala-privacy-check` (defaults to uncommitted+staged changes, or the current HEAD commit if the tree is clean) or `/kabala-privacy-check <commit-sha or range>` to audit something specific.

## Why a separate skill, and why a subagent

The session that just wrote the content is the worst reviewer of it — it already has a reason for every link and name it typed, and shares whatever blind spot let something private through in the first place. (This happened for real: 2026-09-12, a personal Notion URL was committed and pushed to this public repo, caught only because the user asked directly.) This skill exists to break that self-review loop: it hands the diff to a **fresh subagent with zero context about why the content was written**, so it looks at it cold — the way an outside reviewer, or an attacker scanning public repos for leaked links, would.

## Steps

1. **Determine scope.**
   - If a commit SHA or range is given as `$ARGUMENTS`, use `git show <sha>` / `git diff <range>`.
   - Otherwise: `git status --porcelain` + `git diff` + `git diff --staged` for anything uncommitted; if the tree is clean, use `git show HEAD` (the most recent commit).
2. **Collect the changed/added file paths and their full diffs.** For brand-new files the diff already shows the complete content, which is what the subagent needs.
3. **Spawn a subagent** (Agent tool, `general-purpose` or `Explore` type — read-only is enough) with a prompt that is **self-contained and deliberately blind to intent**: hand it only the file paths + diff content, and ask it to check — with no other framing about what the lesson is "about" — for:
   - **Private links** — any URL to a personal/private resource: Notion (`notion.so`, `notion.com`), Dropbox, OneDrive, iCloud share links, or any Google Drive/Docs link that isn't the already-established canonical public lesson source pattern this repo uses (`docs.google.com/document/d/...` cited as the lesson's own source article is expected and fine; a *different*, unexplained personal Drive link is not).
   - **Credentials/secrets** — API keys, OAuth tokens, passwords, anything matching a secret-shaped string near words like `key`/`token`/`secret`/`password`, or raw credential-file content.
   - **Third-party PII** — real people's names, phone numbers, physical addresses, or email addresses — *other than* the repo owner (Anat, `anat.fradin@gmail.com`), figures who are the actual subject matter (Torah/Tanakh figures, named authors like Бааль Сулам/РАБАШ, the named course instructor Л. Веденски — all already used throughout this repo as public attribution), or the instructor's already-public course contact.
   - **Anything else that reads like it was lifted from a private source** — a personal notes export, a personal database dump, internal metadata that has no business in a public Torah/Kabbalah knowledge base.

   Tell the subagent: report each finding as `file — exact snippet — why it's a concern`, or state plainly "clean, nothing found" if there's nothing. It should flag anything borderline rather than assume it's fine — a reviewer who defaults to trust misses exactly what this check exists to catch.
4. **Relay the subagent's verdict.** If invoked as part of `/kabbala-gdoc-lesson`: a "clean" verdict lets the flow continue to the push-confirmation step; any finding blocks it — do not proceed to ask for push confirmation until resolved.
5. **If something is found, fix it before proceeding:**
   - Not yet committed → fix directly in the working tree.
   - Committed but not pushed → fix, then `git commit --amend`.
   - Already pushed → follow the remediation procedure in `CLAUDE.md` § "Privacy & Security": first `git log --all -S"<the sensitive string>"` to see how many commits contain it. Confined to HEAD → `git commit --amend` + `git push --force-with-lease`. Present in older commits too → full `git filter-repo` history rewrite + force-push, which invalidates other clones — explain this plainly and get explicit user confirmation before doing it.
6. **Report the final verdict** to the user: what was checked (file list + scope), what — if anything — was found and how it was fixed, and a clear confirmation that the repo is clean.

## Notes

- This skill is investigation plus, if needed, a small fix — it never pushes on its own. Pushing still goes through the user's normal separate confirmation.
- Keep the subagent's prompt genuinely blind to context. Don't preface it with "this is a Kabbalah lesson about X, please confirm it's fine" — that primes it to rubber-stamp. Hand it the raw diff and ask it to find problems, full stop.
