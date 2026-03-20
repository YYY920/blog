# Personal Profile Site Design

**Date:** 2026-03-20
**Project:** blog (Astro Theme Pure)
**Goal:** Transform the template blog into Jenny Yang's personal profile / job-seeking showcase

---

## Overview

Update the existing Astro blog project to serve as a professional personal profile site, targeting HR and recruiters. The site will highlight work experience, education, projects, and skills. No structural rebuild — all changes reuse existing theme components.

---

## Site Configuration (`src/site.config.ts`)

| Field | Value |
|-------|-------|
| `title` | `Jenny Yang` |
| `author` | `Jenny Yang` |
| `description` | `Full Stack Developer & AI Automation Specialist` |
| `footer.social.github` | `https://github.com/YYY920` |
| Navigation menu | `About / Projects / Blog` (remove Docs and Links) |
| Footer links | Remove Moe ICP link; keep Site Policy |

---

## Homepage (`src/pages/index.astro`)

### Header Area
- Avatar: keep existing
- Name: `Jenny Yang`
- Labels (below name):
  - Location: `Australia`
  - GitHub: `https://github.com/YYY920`
  - LinkedIn: `https://www.linkedin.com/in/yingyu-jenny-yang/`
  - Email: `jennyyang920@gmail.com`

### Section Order (top to bottom)
1. Work Experience
2. Education
3. Projects
4. Skills

> Certifications section removed entirely.

### Work Experience (new section, uses `<Card>` component)

| Company | Title | Location | Period |
|---------|-------|----------|--------|
| Peak Advisory | IT Consultant | Sydney, Australia | Jan 2026 – Present |
| Syncrowin | Software & Digital Twin Engineer | Melbourne, Australia | Feb 2025 – May 2025 |
| TidyTeddy | Full Stack Developer | Sydney, Australia | Nov 2024 – Feb 2025 |
| Schneider Electric | Digital Engineer | Shanghai, China | Sep 2023 – Feb 2024 |

**Peak Advisory bullet points:**
- Collaborated with client to translate business requirements into agentic automation solutions, delivering end-to-end workflows that reduced manual processing time.
- Built an Agentic AI invoice validation agent using n8n, Mistral LLM, automating end-to-end invoice verification with results written to Google Sheets.
- Developed home care RAG pipeline using Postgres, Cohere Reranker, enabling AI-powered querying across PDF, Excel and DOCX documents.

**Syncrowin bullet points:**
- Built RAG-based AI agent to analyse factory documents and deliver responses, reduced information retrieval time, secured a new client partnership.
- Developed interactive dashboards with TypeScript and React, visualizing real-time asset metrics.
- Cleaned and chunked factory documents with Python ETL pipeline.
- Integrated OpenAI embeddings and Qdrant vector database for digital-twin knowledge base search.
- Deployed containerized application to AWS EC2 with Docker, configuring S3 for media storage.
- Wrote unit and integration tests using Jest.

**TidyTeddy bullet points:**
- Created web app using TypeScript, React and Tailwind CSS, reduced WordPress hosting costs and improved maintainability.
- Implemented reusable front-end components with full accessibility support and responsive layouts.
- Developed RESTful services for order processing with TypeScript and Node.js.
- Integrated third party SendGrid API for automated customer confirmation emails.
- Created unit testing with Jest, reduced critical deployment errors by 50%.

**Schneider Electric bullet points:**
- Automated procurement data workflows and reporting with Excel Office Scripts, TypeScript and Power Automate, reduced reporting time from one week to under one hour.

### Education (uses `<Card>` component)

**University of Melbourne** — Victoria, Australia
Master of Information Technology | WAM: 82.17/100 | With Distinction (Top 10%)
Feb 2024 – Dec 2025
- Engineering and IT Graduate Scholarship

**Shanghai University** — Shanghai, China
Bachelor of Computer Science | WAM: 94.95/100 | Dean's List (TOP 1%)
Sep 2019 – Jul 2023
- Academic Excellence Scholarship
- Taekwondo Champion (State Level)

### Projects (rename from "Website List", uses `<ProjectCard>` component)

**video-ops-skill**
Automatically process videos (podcasts/interviews) into publish-ready short clips (9:16 + 1:1), with subtitles and captions. Pipeline: border detection → Whisper.cpp transcription → LLM highlight selection → face tracking → Remotion rendering → social media copy generation.
Tech: Python, Whisper.cpp, LLM, Remotion

**n8n NDIS Invoice Processor**
Automated NDIS invoice processing workflow using n8n, handling validation and data extraction for home care reimbursement.
Tech: n8n, Mistral LLM, Google Sheets

### Skills (uses `<SkillLayout>` component)

| Category | Skills |
|----------|--------|
| Automation & Data | Python, SQL, Excel, Excel Office Scripts, Power Automate, Tableau, ECharts, n8n |
| AI & Agentic AI | Agentic AI, OpenAI API, Mistral, RAG Systems, Postgres, Supabase, Cohere Reranker, AI Coding Copilots |
| Programming | TypeScript, JavaScript, Python, SQL |
| Frameworks & Tools | React, Node.js, FastAPI, RESTful APIs, Express.js |
| Cloud & DevOps | AWS, Microsoft Azure, Docker, GitHub Actions, SharePoint |
| Databases | MySQL, PostgreSQL, MongoDB, Supabase |

---

## About Page (`src/pages/about/index.astro`)

Fill in personal bio integrating README content:
- Full Stack Developer & AI Automation Specialist
- Currently: IT Consultant at Peak Advisory, Sydney
- Education: University of Melbourne (Master of IT, With Distinction)
- Focus: Workflow automation platforms and Agentic AI solutions for real-world business processes

---

## Projects Page (`src/pages/projects/index.astro`)

Showcase the two projects with full descriptions and tech stack tags (same as homepage Projects section).

---

## Deletions / Cleanup

- Remove `Docs` and `Links` from navigation menu in `site.config.ts`
- Remove Moe ICP footer link from `site.config.ts`
- Remove Certifications section from `index.astro`
- Remove Lorem ipsum / placeholder content throughout

---

## What Is NOT Changed

- Theme structure, CSS, component internals
- Blog content (existing posts untouched)
- Build config, Astro config, integrations
- Comment system (Waline), search (Pagefind), RSS

---

## Out of Scope

- Writing actual blog posts
- Custom theme or visual redesign
- New components beyond what the theme provides
