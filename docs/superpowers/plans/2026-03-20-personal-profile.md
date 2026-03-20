# Personal Profile Site Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace all placeholder/template content in the Astro blog with Jenny Yang's real personal profile content, turning it into a job-seeking showcase.

**Architecture:** Content-only updates across 4 files — no new components created. All changes reuse existing astro-pure theme components (`Card`, `ProjectCard`, `SkillLayout`, `Section`, `Label`, `Icon`, `ProjectSection`). Each task is independent and can be verified with `bun run build`.

**Tech Stack:** Astro, astro-pure theme, TypeScript, Bun

**Spec:** `docs/superpowers/specs/2026-03-20-personal-profile-design.md`

---

## File Map

| File | Action | What changes |
|------|--------|--------------|
| `src/site.config.ts` | Modify | title, author, description, github link, nav menu, footer links |
| `src/pages/index.astro` | Modify | header labels, remove Get Template block, replace all sections with real content, keep Posts section |
| `src/pages/about/index.astro` | Rewrite | Remove Hobbies/Tools/Gossips/etc, replace with bio + experience + contact |
| `src/pages/projects/index.astro` | Rewrite | Remove Sponsorship/GPG/GitHub chart/etc, replace with two real projects |

---

## Task 1: Update Site Configuration

**Files:**
- Modify: `src/site.config.ts`

- [ ] **Step 1: Open and read the file**

  Read `src/site.config.ts` to confirm current values before editing.

- [ ] **Step 2: Update title, author, description**

  In the `theme` export object, change:
  ```ts
  title: 'Jenny Yang',
  author: 'Jenny Yang',
  description: 'Full Stack Developer & AI Automation Specialist',
  ```

- [ ] **Step 3: Update GitHub social link**

  Find the `footer.social` object and change:
  ```ts
  social: { github: 'https://github.com/YYY920' }
  ```

- [ ] **Step 4: Replace navigation menu**

  Find `header.menu` and replace the entire array:
  ```ts
  header: {
    menu: [
      { title: 'About', link: '/about' },
      { title: 'Projects', link: '/projects' },
      { title: 'Blog', link: '/blog' }
    ]
  },
  ```

- [ ] **Step 5: Remove Moe ICP footer link**

  In `footer.links`, remove the entry that contains `icp.gov.moe`. Keep only the Site Policy entry:
  ```ts
  footer: {
    ...
    links: [
      {
        title: 'Site Policy',
        link: '/terms',
        pos: 2
      }
    ],
    ...
  }
  ```

- [ ] **Step 6: Verify build passes**

  Run: `bun run build`
  Expected: Build completes with no errors. (The site title and nav will reflect changes.)

- [ ] **Step 7: Commit**

  ```bash
  git add src/site.config.ts
  git commit -m "feat: update site config with Jenny Yang's info and nav"
  ```

---

## Task 2: Rewrite Homepage

**Files:**
- Modify: `src/pages/index.astro`

- [ ] **Step 1: Read the current file**

  Read `src/pages/index.astro` to confirm line numbers before editing.

- [ ] **Step 2: Replace skill variable declarations in frontmatter**

  In the `---` frontmatter block, replace lines 14–16:
  ```ts
  const languages = ['Html', 'JavaScript', 'CSS', 'Shell']
  const frontend = ['TypeScript', 'Vite', 'Webpack', 'Astro']
  const backend = ['Vercel', 'Waline']
  ```
  With:
  ```ts
  const automationData = ['Python', 'SQL', 'Excel', 'Excel Office Scripts', 'Power Automate', 'Tableau', 'ECharts', 'n8n']
  const aiData = ['Agentic AI', 'OpenAI API', 'Mistral', 'RAG Systems', 'Postgres', 'Supabase', 'Cohere Reranker', 'AI Coding Copilots']
  const programmingData = ['TypeScript', 'JavaScript', 'Python', 'SQL']
  const frameworksData = ['React', 'Node.js', 'FastAPI', 'RESTful APIs', 'Express.js']
  const cloudData = ['AWS', 'Microsoft Azure', 'Docker', 'GitHub Actions', 'SharePoint']
  const databasesData = ['MySQL', 'PostgreSQL', 'MongoDB', 'Supabase']
  ```

- [ ] **Step 3: Remove unused imports from frontmatter**

  Remove line 4: `import { Quote } from 'astro-pure/advanced'`

  Update line 7 to remove `Button` (it's only used in the About section being deleted):
  ```ts
  import { Card, Icon, Label } from 'astro-pure/user'
  ```

- [ ] **Step 4: Replace header labels**

  Replace lines 46–57 (the two `<Label>` blocks: "Somewhere" and "Source code") with:
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

- [ ] **Step 5: Remove "Get Template" block**

  Delete lines 60–73 (the `{/* Get template */}` comment and the entire `<a>` block below it ending at `</a>`).

- [ ] **Step 6: Remove the "About" section**

  Delete lines 77–85 (the `<Section title='About'>` block with lorem ipsum text and "More about me" button).

- [ ] **Step 7: Add Work Experience section before the Posts section**

  Insert the following new section immediately before the Posts section (before line 86/the `allPostsByDate.length > 0` block):

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

- [ ] **Step 8: Keep Posts section as-is**

  The existing Posts section (the `allPostsByDate.length > 0 && (...)` block) stays unchanged. Do not touch it.

- [ ] **Step 9: Remove the commented-out Experience block**

  Delete lines 101–129 (the large `{/* <Section title='Experience'>...</Section> */}` commented block).

- [ ] **Step 10: Replace Education section**

  Replace lines 130–148 (the `<Section title='Education'>` block with lorem ipsum) with:
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
      subheading="Bachelor of Computer Science · WAM: 94.95/100 · Dean's List (TOP 1%)"
      date='September 2019 – July 2023'
    >
      <ul class='ms-4 list-disc text-muted-foreground'>
        <li>Academic Excellence Scholarship</li>
        <li>Taekwondo Champion (State Level)</li>
      </ul>
    </Card>
  </Section>
  ```

- [ ] **Step 11: Replace Website List section with Projects**

  Replace lines 150–177 (the `<Section title='Website List'>` block) with:
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

- [ ] **Step 12: Remove Certifications section**

  Delete lines 179–187 (the `<Section title='Certifications'>` block).

- [ ] **Step 13: Replace Skills section**

  Replace lines 189–193 (the `<Section title='Skills'>` block) with:
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

- [ ] **Step 14: Remove `<Quote>` component**

  Delete line 195: `<Quote class='mt-12' />`

- [ ] **Step 15: Verify build passes**

  Run: `bun run build`
  Expected: Build completes with no errors. Homepage shows Work Experience, Posts, Education, Projects, Skills sections.

- [ ] **Step 16: Commit**

  ```bash
  git add src/pages/index.astro
  git commit -m "feat: rewrite homepage with real work experience, education, projects and skills"
  ```

---

## Task 3: Rewrite About Page

**Files:**
- Modify: `src/pages/about/index.astro`

- [ ] **Step 1: Read the current file**

  Read `src/pages/about/index.astro` to confirm full content before rewriting.

- [ ] **Step 2: Overwrite the entire file**

  Replace the entire file contents with:

  ```astro
  ---
  import PageLayout from '@/layouts/CommonPage.astro'

  const headings = [
    { depth: 2, slug: 'about', text: 'About Me' },
    { depth: 2, slug: 'experience', text: 'Experience' },
    { depth: 2, slug: 'contact', text: 'Contact' }
  ]
  ---

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
      <li>Agentic AI &amp; RAG pipelines (n8n, Mistral, OpenAI, Cohere Reranker)</li>
      <li>Full-stack web development (TypeScript, React, Node.js, FastAPI)</li>
      <li>Cloud &amp; DevOps (AWS EC2, Docker, GitHub Actions)</li>
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

- [ ] **Step 3: Verify build passes**

  Run: `bun run build`
  Expected: Build completes with no errors. `/about` renders bio, experience summary, and contact info.

- [ ] **Step 4: Commit**

  ```bash
  git add src/pages/about/index.astro
  git commit -m "feat: rewrite about page with real bio and contact info"
  ```

---

## Task 4: Rewrite Projects Page

**Files:**
- Modify: `src/pages/projects/index.astro`

- [ ] **Step 1: Read the current file**

  Read `src/pages/projects/index.astro` to confirm full content before rewriting.

- [ ] **Step 2: Overwrite the entire file**

  Replace the entire file contents with:

  ```astro
  ---
  import PageLayout from '@/layouts/CommonPage.astro'
  import ProjectSection from '@/components/projects/ProjectSection.astro'

  const headings = [
    { depth: 2, slug: 'projects', text: 'Projects' }
  ]
  ---

  <PageLayout title='Projects' {headings}>
    <h2 id='projects'>Projects</h2>
    <ProjectSection
      projects={[
        {
          name: 'video-ops-skill',
          description: 'Automated video pipeline: given a podcast/interview video, automatically completes border detection & crop → Whisper.cpp transcription → LLM highlight selection → speaker/face tracking → Remotion rendering export (9:16 + 1:1, TikTok subtitles, logo overlay) → social media post copy for each clip.',
          links: [
            { type: 'github', href: 'https://github.com/YYY920/video-ops-skill' }
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

- [ ] **Step 3: Verify build passes**

  Run: `bun run build`
  Expected: Build completes with no errors. `/projects` renders two project entries with GitHub links.

- [ ] **Step 4: Commit**

  ```bash
  git add src/pages/projects/index.astro
  git commit -m "feat: rewrite projects page with video-ops-skill and n8n NDIS processor"
  ```

---

## Final Verification

- [ ] **Run full build one last time**

  Run: `bun run build`
  Expected: Clean build, zero errors.

- [ ] **Optional: Run dev server and visually verify**

  Run: `bun dev`
  Check:
  - Homepage shows: Work Experience (4 entries) → Posts → Education (2 entries) → Projects (2 cards) → Skills (6 categories)
  - Header labels: Australia / GitHub / LinkedIn / email
  - Navigation: About / Projects / Blog
  - `/about` page: bio, experience summary, contact links
  - `/projects` page: two projects with GitHub links
  - No Lorem ipsum text anywhere
  - No "Get Template" button
  - No "Docs" or "Links" in nav
