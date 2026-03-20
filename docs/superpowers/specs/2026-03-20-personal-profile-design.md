# Personal Profile Site Design

**Date:** 2026-03-20
**Project:** blog (Astro Theme Pure)
**Goal:** Transform the template blog into Jenny Yang's personal profile / job-seeking showcase

---

## Overview

Update the existing Astro blog project to serve as a professional personal profile site, targeting HR and recruiters. The site highlights work experience, education, projects, and skills. All changes reuse existing theme components — no new components are created.

---

## 1. Site Configuration (`src/site.config.ts`)

Change the following fields inside the `theme` export object:

| Field path (inside `theme`) | Current value | New value |
|-----------------------------|---------------|-----------|
| `title` | `'Jenny Personal Blog'` | `'Jenny Yang'` |
| `author` | `'Jenny'` | `'Jenny Yang'` |
| `description` | `'Stay hungry, stay foolish'` | `'Full Stack Developer & AI Automation Specialist'` |
| `footer.social.github` | `'https://github.com/cworld1/astro-theme-pure'` | `'https://github.com/YYY920'` |

Change `header.menu` array to (in this exact order):

```ts
[
  { title: 'About', link: '/about' },
  { title: 'Projects', link: '/projects' },
  { title: 'Blog', link: '/blog' }
]
```

In `footer.links`, remove the Moe ICP entry (the one linking to `icp.gov.moe`). Keep only the Site Policy entry.

---

## 2. Homepage (`src/pages/index.astro`)

### 2a. Header Labels

Replace the two existing `<Label>` blocks (location + source code) with these four:

```astro
<Label title='Australia'>
  <Icon name='location' class='size-5' slot='icon' />
</Label>
<Label title='GitHub' as='a' href='https://github.com/YYY920' target='_blank'>
  <Icon name='github' class='size-5' slot='icon' />
</Label>
<Label title='LinkedIn' as='a' href='https://www.linkedin.com/in/yingyu-jenny-yang/' target='_blank' />
<Label title='jennyyang920@gmail.com' as='a' href='mailto:jennyyang920@gmail.com'>
  <Icon name='email' class='size-5' slot='icon' />
</Label>
```

Note: LinkedIn has no built-in icon in astro-pure — use Label without an icon slot (text-only link).

### 2b. Remove "Get Template" block

Delete the `{/* Get template */}` comment block (lines ~61–73 in the original) that links to the theme's GitHub repo.

### 2c. Posts Section (keep as-is)

Keep the existing Posts section that renders recent blog posts (lines using `getBlogCollection`, `sortMDByDate`, `PostPreview`, `allPostsByDate`). Keep its imports: `PostPreview`, `getBlogCollection`, `sortMDByDate`. The existing template blog posts will be replaced by the user's own posts over time — no action required now.

### 2d. Section Order and Content

Remove ALL existing sections EXCEPT the Posts section. Replace with the following sections in this exact order, then append the existing Posts section at the end:

---

#### Section 1: Work Experience (NEW)

```astro
<Section title='Work Experience'>
  <Card
    heading='Peak Advisory'
    subheading='IT Consultant · Sydney, Australia'
    date='January 2026 – Present'
  >
    <ul class='ms-4 list-disc text-muted-foreground'>
      <li>Collaborated with client to translate business requirements into agentic automation solutions, delivering end-to-end workflows that reduced manual processing time.</li>
      <li>Built an Agentic AI invoice validation agent using n8n, Mistral LLM, automating end-to-end invoice verification with results written to Google Sheets.</li>
      <li>Developed home care RAG pipeline using Postgres, Cohere Reranker, enabling AI-powered querying across PDF, Excel and DOCX documents.</li>
    </ul>
  </Card>
  <Card
    heading='Syncrowin'
    subheading='Software & Digital Twin Engineer · Melbourne, Australia'
    date='February 2025 – May 2025'
  >
    <ul class='ms-4 list-disc text-muted-foreground'>
      <li>Built RAG-based AI agent to analyse factory documents and deliver responses, reduced information retrieval time, secured a new client partnership.</li>
      <li>Developed interactive dashboards with TypeScript and React, visualizing real-time asset metrics, enabling instant performance monitoring and anomaly detection.</li>
      <li>Cleaned and chunked factory documents with Python ETL pipeline.</li>
      <li>Integrated OpenAI embeddings and Qdrant vector database for digital-twin knowledge base search.</li>
      <li>Deployed containerized application to AWS EC2 with Docker, configuring S3 for media storage.</li>
      <li>Wrote unit and integration tests using Jest to ensure backend reliability and maintainability.</li>
    </ul>
  </Card>
  <Card
    heading='TidyTeddy'
    subheading='Full Stack Developer · Sydney, Australia'
    date='November 2024 – February 2025'
  >
    <ul class='ms-4 list-disc text-muted-foreground'>
      <li>Created web app using TypeScript, React and Tailwind CSS, reduced WordPress hosting costs and improved maintainability.</li>
      <li>Implemented reusable front-end components with full accessibility support and responsive layouts for mobile and desktop web apps.</li>
      <li>Developed RESTful services for order processing with TypeScript and Node.js, improving concurrency and throughput.</li>
      <li>Integrated third party SendGrid API for automated customer confirmation emails to enhance service delivery.</li>
      <li>Created unit testing with Jest, reduced critical deployment errors by 50%.</li>
    </ul>
  </Card>
  <Card
    heading='Schneider Electric'
    subheading='Digital Engineer · Shanghai, China'
    date='September 2023 – February 2024'
  >
    <ul class='ms-4 list-disc text-muted-foreground'>
      <li>Automated procurement data workflows and reporting with Excel Office Scripts, TypeScript and Power Automate, reduced reporting time from one week to under one hour.</li>
    </ul>
  </Card>
</Section>
```

---

#### Section 2: Education

```astro
<Section title='Education'>
  <Card
    heading='University of Melbourne'
    subheading='Master of Information Technology · WAM: 82.17/100 · With Distinction (Top 10%)'
    date='February 2024 – December 2025'
  >
    <ul class='ms-4 list-disc text-muted-foreground'>
      <li>Engineering and IT Graduate Scholarship</li>
    </ul>
  </Card>
  <Card
    heading='Shanghai University'
    subheading='Bachelor of Computer Science · WAM: 94.95/100 · Dean\'s List (TOP 1%)'
    date='September 2019 – July 2023'
  >
    <ul class='ms-4 list-disc text-muted-foreground'>
      <li>Academic Excellence Scholarship</li>
      <li>Taekwondo Champion (State Level)</li>
    </ul>
  </Card>
</Section>
```

---

#### Section 3: Projects

Rename the section title from "Website List" to "Projects". Use two `ProjectCard` entries. Reuse existing images: `1.avif` for video-ops-skill, `2.avif` for n8n project.

```astro
<Section title='Projects'>
  <div class='grid grid-cols-1 gap-3 sm:grid-cols-2'>
    <ProjectCard
      href='/projects'
      heading='video-ops-skill'
      subheading='Automated video pipeline: podcast/interview → publish-ready short clips (9:16 + 1:1) with subtitles, face tracking, and social media copy.'
      imagePath='/src/assets/projects/1.avif'
    />
    <ProjectCard
      href='/projects'
      heading='n8n NDIS Invoice Processor'
      subheading='Automated NDIS invoice validation and processing workflow using n8n and Mistral LLM, writing results to Google Sheets.'
      imagePath='/src/assets/projects/2.avif'
    />
  </div>
</Section>
```

---

#### Section 4: Skills

Replace placeholder skill arrays with real data:

```astro
const automationData = ['Python', 'SQL', 'Excel', 'Excel Office Scripts', 'Power Automate', 'Tableau', 'ECharts', 'n8n']
const aiData = ['Agentic AI', 'OpenAI API', 'Mistral', 'RAG Systems', 'Postgres', 'Supabase', 'Cohere Reranker', 'AI Coding Copilots']
const programmingData = ['TypeScript', 'JavaScript', 'Python', 'SQL']
const frameworksData = ['React', 'Node.js', 'FastAPI', 'RESTful APIs', 'Express.js']
const cloudData = ['AWS', 'Microsoft Azure', 'Docker', 'GitHub Actions', 'SharePoint']
const databasesData = ['MySQL', 'PostgreSQL', 'MongoDB', 'Supabase']
```

```astro
<Section title='Skills'>
  <SkillLayout title='Automation & Data' skills={automationData} />
  <SkillLayout title='AI & Agentic AI' skills={aiData} />
  <SkillLayout title='Programming' skills={programmingData} />
  <SkillLayout title='Frameworks & Tools' skills={frameworksData} />
  <SkillLayout title='Cloud & DevOps' skills={cloudData} />
  <SkillLayout title='Databases' skills={databasesData} />
</Section>
```

In the frontmatter (`---` block), delete the old variable declarations:
```ts
const languages = [...]
const frontend = [...]
const backend = [...]
```
And add the new skill constant declarations in their place (inside the frontmatter `---` block):
```ts
const automationData = ['Python', 'SQL', 'Excel', 'Excel Office Scripts', 'Power Automate', 'Tableau', 'ECharts', 'n8n']
const aiData = ['Agentic AI', 'OpenAI API', 'Mistral', 'RAG Systems', 'Postgres', 'Supabase', 'Cohere Reranker', 'AI Coding Copilots']
const programmingData = ['TypeScript', 'JavaScript', 'Python', 'SQL']
const frameworksData = ['React', 'Node.js', 'FastAPI', 'RESTful APIs', 'Express.js']
const cloudData = ['AWS', 'Microsoft Azure', 'Docker', 'GitHub Actions', 'SharePoint']
const databasesData = ['MySQL', 'PostgreSQL', 'MongoDB', 'Supabase']
```

---

### 2e. Remove the `<Quote>` component

Delete the `<Quote class='mt-12' />` line at the bottom of the page.

---

## 3. About Page (`src/pages/about/index.astro`)

**Complete rewrite.** Remove all existing sections (Hobbies, Tools, Social Networks, Gossips, About Blog) and replace with the following structure.

New `headings` array:
```ts
const headings = [
  { depth: 2, slug: 'about', text: 'About Me' },
  { depth: 2, slug: 'experience', text: 'Experience' },
  { depth: 2, slug: 'contact', text: 'Contact' }
]
```

New page content:

Keep `import PageLayout from '@/layouts/CommonPage.astro'`. Remove unused imports: `Button`, `Collapse`, `Spoiler`, `Timeline`, `Substats`, `ToolSection`.

The `comment` prop is intentionally removed (no comment section needed on a profile About page).

```astro
<PageLayout title='About' {headings}>
  <h2 id='about'>About Me</h2>
  <p>
    Full Stack Developer and AI Automation Specialist based in Sydney, Australia. Currently working as IT Consultant at Peak Advisory, building agentic AI solutions and workflow automation for real-world business processes in the home care sector.
  </p>
  <p>
    Graduated with a Master of Information Technology (With Distinction, Top 10%) from the University of Melbourne. Experienced across the full stack — from React frontends and Node.js APIs to Python data pipelines, RAG systems, and cloud deployments on AWS.
  </p>

  <h2 id='experience'>Experience</h2>
  <p>
    4 years of experience spanning AI automation, full-stack web development, and digital engineering across Australia and China. Key areas:
  </p>
  <ul>
    <li>Agentic AI & RAG pipelines (n8n, Mistral, OpenAI, Cohere Reranker)</li>
    <li>Full-stack web development (TypeScript, React, Node.js, FastAPI)</li>
    <li>Cloud & DevOps (AWS EC2, Docker, GitHub Actions)</li>
    <li>Data automation (Power Automate, Excel Office Scripts, Python ETL)</li>
  </ul>

  <h2 id='contact'>Contact</h2>
  <ul>
    <li>Email: <a href='mailto:jennyyang920@gmail.com'>jennyyang920@gmail.com</a></li>
    <li>LinkedIn: <a href='https://www.linkedin.com/in/yingyu-jenny-yang/' target='_blank'>linkedin.com/in/yingyu-jenny-yang</a></li>
    <li>GitHub: <a href='https://github.com/YYY920' target='_blank'>github.com/YYY920</a></li>
  </ul>
</PageLayout>
```

---

## 4. Projects Page (`src/pages/projects/index.astro`)

**Complete rewrite.** Remove all template content (Sponsorship, GPG Signature, GitHub activity chart, Learnings, Others sections). Replace with Jenny's two projects using the existing `ProjectSection` component.

New `headings` array:
```ts
const headings = [
  { depth: 2, slug: 'projects', text: 'Projects' }
]
```

New page content:

```astro
<PageLayout title='Projects' {headings}>
  <h2 id='projects'>Projects</h2>
  <ProjectSection
    projects={[
      {
        name: 'video-ops-skill',
        description: 'Automated video pipeline: given a podcast/interview video, automatically completes border detection & crop → Whisper.cpp transcription → LLM highlight selection → speaker/face tracking → Remotion rendering export (9:16 + 1:1, TikTok subtitles, logo overlay) → social media post copy for each clip.',
        links: [
          { type: 'github', href: 'https://github.com/YYY920' }
        ]
      },
      {
        name: 'n8n NDIS Invoice Processor',
        description: 'Automated NDIS invoice validation and processing workflow using n8n and Mistral LLM. Handles end-to-end invoice verification for home care reimbursement, writing validated results to Google Sheets.',
        links: [
          { type: 'github', href: 'https://github.com/YYY920' }
        ]
      }
    ]}
  />
</PageLayout>
```

Keep imports: `import PageLayout from '@/layouts/CommonPage.astro'` and `import ProjectSection from '@/components/projects/ProjectSection.astro'`.

Remove unused imports: `Image`, `Button`, `Collapse`, `Icon`, `Sponsors`, `Sponsorship`, `alipay`, `KeyIcon`, `wechat`.

The `view` prop is intentionally removed from `<PageLayout>` (page-view counter not needed on a personal profile site).

Also remove the `<style>` block at the bottom of the file (it was only used by the now-deleted Sponsorship component).

---

## 5. Deletions Summary

| Location | What to remove |
|----------|---------------|
| `site.config.ts` | Moe ICP footer link (nav changes are handled by the new `header.menu` array in Section 1) |
| `index.astro` | "Get Template" button block; old skill variable declarations (`languages`, `frontend`, `backend`); Certifications section; existing "About" section; all placeholder sections (Skills, Education, Website List); `<Quote>` component at bottom |
| `about/index.astro` | All existing sections (Hobbies, Tools, Social Networks, Gossips, About Blog) and their unused imports |
| `projects/index.astro` | All existing sections (Sponsorship, GPG Signature, GitHub chart, Learnings, Others, Programs), unused imports, and the `<style>` block |

---

## 6. What Is NOT Changed

- Theme structure, CSS, component internals
- Blog content (existing posts untouched)
- Build config (`astro.config.ts`), integrations
- Comment system (Waline), search (Pagefind), RSS feed
- `public/` assets (favicon, social card image)
- Avatar image (`/src/assets/avatar.png`) — keep as-is unless user provides new one

---

## 7. Out of Scope

- Writing actual blog posts
- Custom theme or visual redesign
- New Astro components
- Deploying to production
- Updating avatar image (user to handle separately if desired)
