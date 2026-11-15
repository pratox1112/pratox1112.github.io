# Portfolio Site Roadmap

**Owner:** Pratosh Karthikeyan
**Site:** https://pratox1112.github.io (GitHub Pages user site)
**Repo:** `pratox1112/pratox1112.github.io`
**Status:** Planning
**Last updated:** Nov 13, 2026

---

## How to use this file (instructions for Claude Code)

- Work one phase at a time, in order. Stop at the end of each phase so I can review before you start the next one.
- Check off tasks (`- [x]`) as you finish them, and commit and push `redesign` at the end of each phase with a message naming it, e.g. `phase 2: scaffold pages and shared layout`.
- **Do not invent content.** Every claim and number on the site must come from my resume (Appendix A) or a repo README I point you to. If something is missing, insert a visible placeholder like `[TODO: p95 latency]` and add it to **Open questions** at the bottom of this file.
- Do not touch anything outside this repo.
- Ask before adding any dependency, external script, CDN link, or build tool.
- All work happens on the `redesign` branch. Do not commit to the default branch until Phase 7 (launch).

---

## Goal

A fast, simple portfolio that an MLE recruiter or hiring manager can skim in under a minute and come away knowing three things: what I build, my two strongest projects with real results, and how to reach me. It will be linked from my resume header, replacing datascienceportfol.io.

**Done means:** live at pratox1112.github.io, works well on a phone, supports light and dark mode, has two complete case studies, and every number on it is traceable to a source.

---

## Decisions already made

- **Hosting:** GitHub Pages, deploying from the default branch, root folder.
- **Stack:** plain HTML and CSS, with minimal vanilla JS only where it's actually needed. No framework, no build step, no npm. (Revisit Astro only if I start writing regular posts.)
- **`.nojekyll`** at the repo root so GitHub serves files as-is.
- **No runtime dependencies.** The site must work with no external scripts. Fonts are self-hosted in `assets/fonts/` or use a solid system font stack.
- **Source of truth:** my resume, for wording and numbers.
- **Mayo Clinic work:** resume-level detail only. No code, data, screenshots, patient information, or internal details beyond what's already on the resume until I confirm with my former supervisor.
- **Contact:** email `pratoshk993@gmail.com` (matches resume), GitHub, LinkedIn. No phone number on the public site.
- **Branching:** `old-site` holds a backup of the current site; `redesign` holds all new work; the default branch keeps the old site live until launch.

---

## Phase 1: Back up and prepare the repo

- [x] Clone `https://github.com/pratox1112/pratox1112.github.io.git`
- [x] Confirm the default branch name (`main` or `master`) and use it everywhere below
- [x] Create an `old-site` branch from the default branch and push it (permanent backup)
- [x] Create a `redesign` branch from the default branch; do all further work here
- [x] On `redesign`, remove the old site files
- [x] Add `.nojekyll` (empty), a one-line `README.md` describing the repo, and this `ROADMAP.md`
- [x] Commit and push `redesign`: `phase 1: back up old site, start redesign branch`

---

## Phase 2: Scaffold the structure

Target layout:

```
pratox1112.github.io/
├── index.html            # home page
├── 404.html              # not-found page with a link home
├── styles.css            # shared styles for every page
├── .nojekyll
├── README.md
├── ROADMAP.md
├── assets/
│   ├── resume.pdf
│   ├── favicon.svg
│   ├── og-image.png      # 1200×630 preview image for link sharing
│   ├── fonts/
│   └── images/           # diagrams, screenshots (compressed)
└── projects/
    ├── brainct.html
    └── nl2sql.html
```

- [x] Create every file with valid HTML5 boilerplate: `lang="en"`, `charset`, viewport meta tag
- [x] Shared header (nav) and footer, identical on every page. Copy-paste is fine; no templating.
- [x] Per-page `<title>` and meta description
- [x] Open Graph and Twitter card tags so the link previews properly on LinkedIn
- [x] Favicon
- [x] `404.html` with a link back home
- [x] Placeholder content everywhere; real content comes in Phase 6
- [x] Commit: `phase 2: scaffold pages and shared layout`

---

## Phase 3: Design system

**Brief**

- **Subject:** an ML engineer who works across medical imaging, LLM systems, and production MLOps.
- **Audience:** recruiters and MLE hiring managers skimming quickly, often on a phone, arriving from my resume or LinkedIn.
- **Primary job:** get the visitor into a project case study or to my contact details.

**Process**

- [x] Before writing any CSS, propose a short design plan for my approval:
  - 4–6 named hex colors, with light and dark values
  - typefaces and their roles (one or two families, clearly distinct if two)
  - a type scale
  - a layout concept, with ASCII wireframes of the home page and a case-study page, including alignment
  - 2–3 principles that make this site specific to me rather than a generic template
- [x] Review the plan against the brief and revise anything that reads like a default template. Avoid:
  - warm cream background with a serif display and a terracotta accent
  - near-black background with a single neon accent
  - content chopped into identical rounded cards with the same soft gray shadow and gradient washes
  - all-caps eyebrow labels above every heading
  - numbered markers (01 / 02 / 03) on content that isn't a sequence
  - fade-and-slide-in animations on every section
- [x] Spend the boldness in one place (for example, how results are presented, or the intro). Keep everything else quiet.
- [x] Implement colors and type as CSS custom properties on `:root`, with dark values under `@media (prefers-color-scheme: dark)`
- [x] Quality floor:
  - responsive down to 360px wide; no sideways scrolling (wide tables and code scroll inside their own container)
  - body text line length under about 75 characters
  - visible keyboard focus states
  - respects `prefers-reduced-motion`
  - WCAG AA contrast in both themes
- [x] Commit: `phase 3: design system`

**Approved design (Nov 15, 2026)**

- **Concept:** a technical report, not a landing page. Results are the one loud element: large IBM Plex Mono figures (`.figures`), each with a caption saying how it was measured. Hairline rules and space instead of cards.
- **Colors (light / dark):** Paper `#FBFBFA` / `#14171C`, Ink `#1B1F24` / `#E6E8EB`, Graphite `#5B6470` / `#9AA3AE`, Hairline `#DADDE1` / `#2A2F36`, Signal `#24489E` / `#9DB7F5`, Signal tint `#EEF1F8` / `#1B2130`. All text pairs pass WCAG AA; all but light Graphite (5.8:1) pass AAA.
- **Type:** system sans for text; self-hosted IBM Plex Mono 400/600 (`assets/fonts/`, SIL OFL) for figures, tables and dates. Scale: 14 / 17 / 20 / 25 / 30–42 / 36–52 (figures) px.
- **Components in `styles.css`:** `.section` (heading + rule), `.lede`, `.inline-links`, `.figures`, `.project`, `.entry` / `.entry-head` / `.entry-role`, `.pairs`, `.back-link`, `.diagram`, `.decision`, `.table-wrap` + `td.value`, `.todo`.

---

## Phase 4: Home page

Sections, in this order:

1. **Header:** my name, nav links to Projects, Experience, Resume (PDF), Contact
2. **Intro:** name, a one-line positioning statement, two or three sentences about what I build, links to GitHub, LinkedIn, resume, and email
3. **Featured projects:** BrainCT and Agentic NL2SQL. For each: a two-sentence summary, two or three headline results, and links to the case study and the repo
4. **Experience:** Mayo Clinic, Ideatec Softwares, Diggibyte Technologies. Role, dates, and two or three condensed lines each
5. **Skills:** grouped the same way as the resume, compact
6. **Education:** Northeastern MS ECE (Dec 2026), Sri Venkateswara College of Engineering BE
7. **Footer:** email, GitHub, LinkedIn, last-updated date

Tasks:

- [x] Build all sections with placeholder copy
- [x] Draft 2–3 options for the positioning line for me to choose from. No title inflation: I'm finishing an MS, so no "Senior" or "Lead".
- [x] Resume link opens `assets/resume.pdf` in a new tab
- [x] Commit: `phase 4: home page structure`

---

## Phase 5: Case-study page template

Build the structure in `projects/brainct.html` with placeholders, then copy it to `projects/nl2sql.html`.

Sections, in this order:

1. **Title** and a one-sentence summary
2. **At a glance:** my role, stack, timeframe, links (repo, demo if any)
3. **Problem:** what it is and why it's hard
4. **Architecture:** a diagram (SVG or compressed PNG in `assets/images/`) plus a short walkthrough
5. **Key decisions:** 2–4 of them. For each: the choice, the alternatives I considered, and why I chose this
6. **Results:** a table with metric, value, and how it was measured (dataset and split, hardware, load profile)
7. **What didn't work / what surprised me**
8. **What I'd do next**
9. **Links:** repo, demo, related writing

Tasks:

- [x] Build the template with placeholders in every section
- [x] Results table scrolls horizontally inside its own container on small screens
- [x] "Back to projects" link at the top and bottom
- [x] Commit: `phase 5: case-study template`

---

## Phase 6: Content

Fill from Appendix A first, then enrich from the repo READMEs. Anything not in a source gets a `[TODO]` placeholder.

- [ ] **Home page:** replace all placeholder copy using Appendix A
- [ ] **BrainCT case study:** source is the BrainCT repo README (URL in Open questions)
- [ ] **NL2SQL case study:** source is the NL2SQL repo README (URL in Open questions)
- [ ] **Mayo Clinic:** experience entry at resume-level detail only; no separate page for now
- [ ] **Architecture diagrams** for both projects, exported to `assets/images/`
- [ ] **Resume PDF** copied to `assets/resume.pdf` (current MLE version)
- [ ] **OG preview image** created at 1200×630
- [ ] Resolve or list every remaining `[TODO]` under Open questions
- [ ] Commit: `phase 6: content`

---

## Phase 7: QA and launch

**Local preview**

```bash
python -m http.server 8000
# open http://localhost:8000
```

**QA checklist**

- [ ] Every link works: nav, project links, repo links, resume PDF, email, 404 page
- [ ] Looks right at 360px, 768px, and desktop widths
- [ ] Light and dark mode both readable
- [ ] Full keyboard navigation with visible focus
- [ ] No console errors
- [ ] Images compressed; total page weight kept small
- [ ] Lighthouse run on home page and one case study; fix anything flagged in accessibility and performance
- [ ] No `[TODO]` placeholders left on the pages
- [ ] Link preview checked (paste the URL into a LinkedIn post draft without posting)

**Launch**

- [ ] Merge `redesign` into the default branch and push
- [ ] Repo Settings → Pages: Source set to "Deploy from a branch," default branch, `/ (root)`. "Enforce HTTPS" checked.
- [ ] Actions tab: wait for "pages build and deployment" to go green
- [ ] Visit https://pratox1112.github.io and hard-refresh (Ctrl+Shift+R / Cmd+Shift+R)
- [ ] Re-run the link check on the live site

---

## Phase 8: After launch

- [ ] Resume: replace the datascienceportfol.io link with pratox1112.github.io; make sure all resume links are real hyperlinks
- [ ] LinkedIn: add the site to the profile's contact info and Featured section
- [ ] GitHub profile cleanup:
  - [ ] Pin BrainCT, NL2SQL, and the best one or two other repos
  - [ ] Replace the default profile README with one that matches the site
  - [ ] Fix the email on the profile README (it currently shows a different address than the resume)
  - [ ] Each pinned repo's README has a diagram, headline results, and a "how to run" section

---

## Phase 9: Later (optional)

- [ ] **BrainCT live demo** on Hugging Face Spaces using the ONNX INT8 model on CPU, embedded in the case study. Check the dataset's license terms before hosting any sample scans.
- [ ] **NL2SQL demo:** a recorded GIF or short video of the agent routing a failed query (a live demo would cost LLM API calls)
- [ ] **Short write-ups**, one per finding:
  - INT8 accuracy cost depends on CPU support (VNNI vs no VNNI)
  - micro-batching only helps under overload
  - domain hints and the paired McNemar test
- [ ] **Custom domain** (e.g., pratosh.dev): add under Settings → Pages → Custom domain and set DNS at the registrar
- [ ] **Privacy-friendly analytics**, if I want to know whether anyone visits
- [ ] **New project pages** as projects ship, using the Phase 5 template
- [ ] Reconsider Astro only if posts become regular

---

## Not in scope

- Frameworks, CMSs, or build pipelines
- A contact form or any backend
- A blog engine (write-ups are plain HTML pages for now)
- A separate Mayo Clinic case study (until cleared)

---

## Open questions

1. ~~**BrainCT repo URL:** probably `github.com/pratox1112/BrainCT-Hemorrhage-MLOps`. Confirm.~~ Resolved: the public repo exists at that URL and is linked from the home page.
2. **NL2SQL repo URL:** probably `github.com/pratox1112/nl2sql-agentic-rag` (the only public NL2SQL repo); linked from the home page for now. Confirm.
3. **W&B on BrainCT:** the resume says BrainCT tracks training runs in W&B. Confirm against the repo. If it doesn't use W&B, remove that from the site and the resume.
4. **NL2SQL evaluation set sizes:** 44.20% is on 500 BIRD-SQL questions, but the domain-hints comparison (44.00% → 52.67%) doesn't divide evenly into 500; those percentages fit a 150- or 300-question subset. Confirm the subset size and state it on the case study so the numbers don't look inconsistent.
5. **Mayo Clinic:** what can be said publicly beyond the resume? Is there a poster, abstract, or paper to link?
6. **Headshot:** include one or not?
7. ~~**Old site:** is anything on the `old-site` branch worth carrying over?~~ Resolved: the old site was a single digital-clock demo page; nothing to carry over.

---

## Appendix A: Source facts from the resume

Use these as written. Do not round, extrapolate, or add numbers that aren't here.

**Contact**
- Pratosh Karthikeyan, Boston, MA
- pratoshk993@gmail.com
- linkedin.com/in/pratosh-karthik
- github.com/pratox1112

**Education**
- Northeastern University, MS Electrical and Computer Engineering, Aug 2024 – Dec 2026, GPA 3.8/4.0. Concentration: Computer Vision, Machine Learning and Algorithms.
- Sri Venkateswara College of Engineering (Anna University), BE Electronics and Communications Engineering, Jun 2020 – Jun 2024, Chennai, India.

**Mayo Clinic, Data Science Intern (Jan 2026 – Aug 2026, Rochester, MN)**
- Pretrained DINOv3 (ViT-G, ViT-H) pathology foundation models with self-supervised learning on 1,500 ovarian cancer WSIs (18.2M tiles) across 8 H100 GPUs on a Slurm cluster; tuned SSL hyperparameters for large-scale training.
- Engineered a whole-slide imaging pipeline (OpenSlide, CLAM) to tile slides at multiple magnifications.
- Benchmarked DINOv3 checkpoints against UNI2 and Virchow2 with a PyTorch linear-probing pipeline on held-out data; ViT-G at 10x was the strongest in-house configuration.
- Designed a clinical trial eligibility screener automating criterion-by-criterion review of patient records with Gemini 2.5 Pro and LLaMA 3.1, producing per-criterion reasoning so each decision is auditable.
- Built per-criterion LLM orchestration with a GraphRAG layer: 100% sensitivity at 75% specificity on 1,000 patients with known eligibility.
- Served LLaMA 3.1 70B with vLLM on 4 A100 GPUs under Slurm: 500 tokens/s at 2s average latency per request.

**Ideatec Softwares, Data Science Intern (Jan 2024 – May 2024, Chennai)**
- End-to-end AWS pipeline (S3, Glue, SageMaker) scoring 5 sensors at 5-minute intervals for anomaly detection, trained on a month of readings.
- Anomaly detection models (Autoencoders, Isolation Forest, DBSCAN) reaching 95% precision on labeled machine breakdown events; EDA-driven feature changes raised recall from 74% to 92%.
- Automated data quality checks and drift monitoring.
- Worked cross-functionally with data engineering and ML teams to harden and scale models in production.

**Diggibyte Technologies, Data Engineering Intern (Mar 2023 – Apr 2023, Bangalore)**
- ADF and Databricks pipeline for nested REST API JSON in PySpark and Delta Lake, cutting processing time 40%.
- Reusable PySpark data models persisted in Delta Lake; ETL orchestrated with Airflow.

**BrainCT: Intracranial Hemorrhage Detection, End-to-End MLOps**
- From 752,803 raw DICOMs to a load-tested GKE service.
- 0.977 macro AUC (95% CI 0.973–0.980) on a patient-level held-out set.
- ONNX INT8 cut latency 4.9×; accuracy cost depends on CPU support: −0.0013 AUC with VNNI vs −0.0073 without.
- Served via FastAPI: p95 38.6 ms, 420 tests.
- Micro-batching adds 55% throughput only under overload.
- Autoscaling from 1 to 3 pods sustained 24.2 req/s at p95 207 ms with 0 errors.
- (See Open question 3 about W&B before using it.)

**Agentic NL2SQL: Self-Correcting Multi-Agent Text-to-SQL**
- Five-agent LangGraph state machine turning plain-English questions into SQL; routes each failed query to the agent responsible for the error instead of re-prompting blindly.
- 44.20% accuracy on 500 BIRD-SQL benchmark questions.
- Exposed as a 7-tool MCP server with read-only guardrails enforced at the tool boundary, verified across 1,132 benchmark statements with 0 false rejections.
- Domain hints raised accuracy from 44.00% to 52.67%, paired McNemar test p = 0.0072. (See Open question 4.)
- 119 tests, GitHub Actions CI.

**Skills (grouped as on the resume)**
- Programming: Python (Pandas, NumPy, Scikit-Learn), SQL, R, PySpark, Git, GitHub Actions CI/CD
- Machine Learning: Classification, Regression, Clustering, Anomaly Detection, Uplift Modeling, LightGBM, EconML
- Deep Learning: PyTorch, CNN (ResNet), Vision Transformers, Self-Supervised Learning, ONNX Runtime, Quantization
- LLMs & GenAI: vLLM, RAG, GraphRAG, LLM Evaluation, LangGraph, MCP, LangChain, Hugging Face
- MLOps & Serving: FastAPI, Docker, Kubernetes (GKE), Helm, Terraform, Prometheus, Grafana, Locust, MLflow, W&B
- Data & Cloud: AWS (S3, SageMaker, Glue), GCP, Databricks, Airflow, Snowflake, dbt, Slurm (Multi-GPU)
