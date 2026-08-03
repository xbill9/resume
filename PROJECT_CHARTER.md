# Project Charter: Resume Automation & Maintenance

**Project Manager:** [xbill@glitnir.com](mailto:xbill@glitnir.com)  
**Start Date:** 2026-07-19  
**End Date:** 2026-12-31  

---

### Project Goals
* **Source of Truth:** Maintain all resume content in `resume_consolidated.md` as a single, version-controlled source.
* **ATS Optimization:** Ensure all generated `.docx` files are 100% compliant with Applicant Tracking Systems (no tables, ASCII only).
* **Privacy & Security:** Automate the scrubbing of PII (Phone/Address) from public commits using git hooks and the `PRIVATE_CONTACT` file.
* **Tailoring Efficiency:** Use the `jd-match` tool to rapidly adapt the 2-page resume variant for specific job descriptions.

### Timeline
* **Phase 1: Pipeline Stabilization** (July 2026) - Finalize `make-resume` script and PDF/DOCX consistency.
* **Phase 2: GDE/AWS Spotlight Integration** (August 2026) - Update metrics and public artifacts for 2026 honors.
* **Phase 3: Automated Google Docs Sync** (September 2026) - Enhance `push-gdocs` for stable cloud editing.

### Budget
* **Software:** $0 (Open Source: Python, LibreOffice, Pandoc/md2docx).
* **Hosting:** $0 (GitHub, Hugging Face, Google Drive).
* **Infrastructure:** Vertex AI / TPU v6e (via Google Developer Expert program credits).

---

### Document Summary
This charter outlines the technical roadmap for the `xbill/resume` repository, focusing on agentic automation and cross-platform visibility for William McLean's professional profile.
