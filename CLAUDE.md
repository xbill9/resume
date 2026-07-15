# CLAUDE.md

Resume repo for William McLean (xbill / xbill9). Markdown sources build to DOCX (ATS uploads) and PDF (humans) via `./make-resume`.

## Structure

- `resume_consolidated.md` — master, 3 pages. Source of truth.
- `resume_2page.md` — condensed variant, **must stay exactly 2 pages**. When the master changes materially, port the change here in compressed form.
- Generated files (`.docx`, `.pdf`, `.txt`) are committed; regenerate them in the same commit as any `.md` edit.

## Build & verify

```bash
./make-resume                  # master
./make-resume resume_2page.md  # 2-pager
```

The script prints the page count and a hunspell report. All currently flagged words are proper nouns/tech terms — investigate any new flag.

## Formatting rules (ATS)

- ASCII only for punctuation: straight quotes, plain hyphens in dates (`2002 - Present`). No curly quotes, no `\-` escapes, no backticks (use **bold** for repo/tool names).
- No tables, columns, images, or emoji in resume content.
- Job entries are three lines: bold title / `Company, City, ST` / date range. Education: bold degree line, then school line. Contact lines use labels (`Phone:`, `Email:`, `LinkedIn:`).
- Spell out acronym + full form at least once each (e.g., "Model Context Protocol (MCP)", "Tensor Processing Units / TPU").
- Section headers stay conventional: Professional Summary, Core Competencies & Skills, Certifications & Developer Programs, Professional Experience, Education, Publications.

## Contact-info policy (privacy — do not violate)

This repo is **public**. Committed files carry only email + city/state/ZIP — never the phone number or street address. The full contact line lives in the gitignored `PRIVATE_CONTACT` file; `./make-resume` automatically builds full-contact `.docx`/`.pdf` into the gitignored `private/` directory — those are the versions to submit with applications. Never commit `PRIVATE_CONTACT`, anything under `private/`, or a phone/street address in any file.

## Content rules (accuracy — do not violate)

- **Never invent metrics.** Unmeasured percentages were deliberately removed. Every number must be verifiable: $20M+ transactions, 99.9% availability, 15+ years PCI-DSS, 300+ articles, 170+ repos, ~1,000 Docker pulls (refresh from hub.docker.com/u/xbill9 when touching that line).
- Gemma 4 on AWS Inferentia2 is the "**first community port**" — not "first port".
- Google Cloud Next 2026: William **TA'd a post-event workshop** on the keynote demos. He did not author the keynote code and was not a keynote TA. The `next26` repo is Google's demo code, not his.
- Claims should trace to public artifacts: github.com/xbill9, huggingface.co/xbill9, hub.docker.com/u/xbill9, dev.to/xbill, medium.com/@xbill999.
- GDE advocate role dates from 2024. AWS recognition wording: "five-time AWS Community Builder Spotlight honoree (5-Timers Club)".

## Tailoring workflow

For a specific job posting: save the posting to `private/jd/<company>.txt`, run `./jd-match private/jd/<company>.txt` to see covered vs. missing keywords, then copy `resume_2page.md` to a new file under `private/`, mirror the posting's job title in the headline line, add missing keywords **only where honest**, and build with `./make-resume private/<file>.md` — never edit the master for a one-off application.

## Repo tooling

- `hooks/pre-commit` (enabled via `git config core.hooksPath hooks`) blocks commits containing phone numbers or the street address, including inside .docx/.pdf binaries. If it fires, fix the content — never bypass with `--no-verify`.
- `jd-match` is stdlib-only Python; keep it dependency-free.
