# Resume

Source-controlled resume for **William McLean** ([xbill9](https://github.com/xbill9)) with a reproducible Markdown → DOCX → PDF build pipeline, optimized for ATS parsers and application-site importers.

## Files

| File | Purpose |
|---|---|
| `resume_consolidated.md` | **Master resume** (3 pages) — the source of truth. Full detail: all projects, talks, and publications. |
| `resume_2page.md` | Trimmed 2-page variant for recruiters and human readers. |
| `*.docx` | Generated Word versions — **upload these to application sites** (best parser compatibility). |
| `*.pdf` | Generated PDF versions — for email and human eyes. |
| `*.txt` | Extracted PDF text layer — exactly what an ATS parser sees. |
| `md2docx.py` | Markdown → DOCX converter (python-docx). ATS-safe output: real heading styles, no tables, clickable hyperlinks, compact spacing. |
| `make-resume` | One-command build: docx + pdf + text layer + page count + spell check. Also builds full-contact copies into `private/`. |
| `jd-match` | Compare a job posting's keywords against the resumes: `./jd-match private/jd/posting.txt` reports covered vs. missing terms. |
| `jd-search` | Search Google Careers for postings, filter by location, rank by keyword hits, and `--save` them into `private/jd/` for `jd-match`. |
| `hooks/pre-commit` | PII guard — blocks any commit containing a phone number or street address (scans inside .docx/.pdf too). Enable with `git config core.hooksPath hooks`. |

## Build

```bash
./make-resume                  # build the master
./make-resume resume_2page.md  # build the 2-page variant
```

### Dependencies (Debian)

```bash
sudo apt install python3-docx libreoffice-writer-nogui poppler-utils \
                 fonts-crosextra-carlito hunspell hunspell-en-us
```

`fonts-crosextra-carlito` matters: the DOCX uses Calibri, and Carlito is its metric-compatible substitute, so LibreOffice's PDF export keeps identical line breaks and page counts.

## Setting up on a new machine

The full-contact builds are never in git — they regenerate locally from `PRIVATE_CONTACT`:

1. `git clone https://github.com/xbill9/resume.git` and install the dependencies above.
2. Recreate `PRIVATE_CONTACT` at the repo root: a single-line file holding the full contact line (phone + street address) that replaces the public contact line. Transfer it over a channel that isn't git — `scp`, a USB stick, or a password manager — e.g. `scp oldhost:resume/PRIVATE_CONTACT resume/`.
3. Enable the PII guard: `git config core.hooksPath hooks`.
4. Run `./make-resume` and `./make-resume resume_2page.md` — the full-contact `.docx`/`.pdf` land in the gitignored `private/` directory. Those are the versions to submit with applications.

Never `git add -f` anything under `private/` or `PRIVATE_CONTACT`, and don't move the built files through anything that syncs publicly.

## Conventions

- Tailoring for a posting: `./jd-search "customer engineer AI" -l "New York, NY, USA" -m agent agentic --save` pulls matching Google Careers postings into the gitignored `private/jd/`, then `./jd-match private/jd/<slug>.txt` shows covered vs. missing keywords.
- Edit only the `.md` files; everything else is generated. Rebuild after every edit and check the page count (`resume_2page` must stay at 2 pages).
- ATS formatting rules and content rules live in [CLAUDE.md](CLAUDE.md) / [GEMINI.md](GEMINI.md).
- **Privacy:** committed files are scrubbed (email + city/state only). Full-contact versions for actual applications are built automatically into the gitignored `private/` directory from the gitignored `PRIVATE_CONTACT` file.

## Links

[LinkedIn](https://www.linkedin.com/in/xbill) · [GitHub](https://github.com/xbill9) · [Hugging Face](https://huggingface.co/xbill9) · [Docker Hub](https://hub.docker.com/u/xbill9) · [dev.to](https://dev.to/xbill) · [Medium](https://medium.com/@xbill999)
