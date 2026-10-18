# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Serhii Burlaka's personal web CV, hosted on GitHub Pages (`SergioBurlaka.github.io`, served from `master`). Static site: no package manager, no build step, no tests, no linter. Pushing to `master` publishes the site, so don't commit or push without an explicit request.

The user communicates in Ukrainian; answer in Ukrainian. CV content itself is written in English.

## Structure

- `index.html` — the live site: a single-column, ATS-friendly, print-ready (A4) CV with all CSS inline and no external dependencies. The user edits this file directly.
- `cv/` — the CV deliverables:
  - `Serhii_Burlaka_CV.html` — a copy of `index.html`.
  - `Serhii_Burlaka_CV.md` — the same content as Markdown.
  - `Serhii_Burlaka_CV.pdf` — generated from the HTML.
  - `CHANGES.md` — what changed vs. the old CV, where facts came from, open items.
- Legacy files from the old two-column site, no longer referenced by `index.html`: `main.css`, `script.js`, `js/` (jQuery), `lib/` (Font Awesome, Roboto, ArtStation logos), `images/`, `Burlka Resume_8.pdf` (old CV), `cv-content.odt`, `letter_1.odt`.
- `CV_TASK.md` (untracked) — the original brief for the CV rewrite; the rewrite is done, but its rules still apply.

## Editing the CV

Keep `index.html`, `cv/Serhii_Burlaka_CV.html` and `cv/Serhii_Burlaka_CV.md` in sync. If the user edited one of them, treat it as the source and propagate to the others. Diff `index.html` against `cv/Serhii_Burlaka_CV.html` first to see what they changed.

Regenerate the PDF with headless Chrome (PowerShell). It must stay at 2 pages A4 or fewer:

```powershell
$root = "C:\Users\Envy17\Project\SergioBurlaka.github.io"
& "C:\Program Files\Google\Chrome\Application\chrome.exe" --headless=new --disable-gpu --no-pdf-header-footer "--print-to-pdf=$root\cv\Serhii_Burlaka_CV.pdf" "file:///$($root -replace '\\','/')/index.html"
```

Content rules from the brief:
- Never invent metrics, technologies or responsibilities. Every claim must come from the old CV, project code, or the user. If unsure, mark it `[TODO: ...]` and ask.
- Use past-tense, verb-first bullets, and dates in `Mon YYYY – Mon YYYY` format.

Decisions already made by the user:
- Name is spelled "Serhii".
- No War Thunder / 3D artist entry.
- No PHP/Symfony backend work (the CV stays frontend-oriented).
- English level "Intermediate", remote format.
- The MyGym link uses the bare IP until there is a domain.

## Sources of facts (sibling repos in `C:\Users\Envy17\Project\`)

- `New_delikeys_frontend_2` — Delikeys 2.0 frontend (Maya B, Mar 2024 – present). The user started it on 2024-04-08 and authored most commits.
- `new-delikeys-2` — Delikeys PHP/Symfony backend (deliberately excluded from the CV).
- `seo-management-tool` — Brightgrove project. The user's first commit there (2022-11-23) is the basis for the "Nov 2022" start date.
- `MyGym` — full-stack pet project listed under Projects.

Never read `.env*` files or the key/certificate files in the `Brightgrove` folder.
