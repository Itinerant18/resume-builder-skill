---
name: resume-builder
description: Build a professional, ATS-optimized LaTeX + PDF resume by combining data from a user's GitHub profile, LinkedIn export, LeetCode account, Figma profile, and portfolio website. Use this skill whenever the user wants to create or generate a resume, CV, or wants to turn their profiles into a document. Trigger on phrases like "build my resume", "make a resume from my GitHub", "create a CV", "generate a resume from my profiles", "resume from LinkedIn and GitHub", "help me get shortlisted", "optimize my resume for ATS", or any mention of combining developer, designer, or professional profiles into a resume. Even if the user only mentions one or two profiles, still use this skill. Also trigger when user attaches or shares a portfolio URL alongside resume-building intent.
---

# Resume Builder Skill

Builds a polished, ATS-optimized, 2-column 1-page resume in both `.tex` (LaTeX source) and `.pdf` formats. Pulls structured data from GitHub, LinkedIn, LeetCode, Figma, and the user's personal portfolio website. The final output is engineered to pass ATS screening and catch a recruiter's eye within 6 seconds.

---

## Step 1: Gather Inputs

Ask the user for all of the following **in a single message** — do not ask one by one:

**Profile sources:**
1. **GitHub username or URL** — e.g., `github.com/johndoe` or just `johndoe`
2. **LinkedIn export text** — paste from About, Experience, Education, Skills, and Certifications
3. **Portfolio / personal website URL** (strongly recommended) — e.g., `johndoe.dev`, `johndoe.github.io`, Notion, Behance, or any personal site
4. **LeetCode username** (optional, for developers / competitive programmers)
5. **Figma username** (optional, for UI/UX designers)

**Personal contact info:**
6. Full name, email, phone, location/city

**Role targeting:**
7. **Target job title** — e.g., "Senior Frontend Engineer", "Product Designer"
8. **Target company** (optional)
9. **Job description** (optional but strongly recommended) — paste full JD for ATS keyword optimization
10. **Resume style** — ask them to choose:
    - `navy-gold` — Deep navy + gold accent. Most universally shortlisted. Works for tech, finance, consulting, product.
    - `slate-teal` — Charcoal slate + teal accent. Popular at startups and design-forward companies.
    - `midnight-coral` — Near-black + warm coral. Striking and modern, excellent for creative/product roles.
    - `classic-mono` — Pure black and white, maximum ATS safety. Use for conservative industries (banking, law, government).

---

## Step 2: Fetch and Parse Portfolio Website (Primary Source)

If the user provided a portfolio URL, use `web_fetch` to retrieve it. Extract:

- **Projects / case studies**: title, description, tech stack, outcomes, links
- **Skills and tools** mentioned or demonstrated
- **Bio or About text**: use as a source for the Summary section
- **Testimonials or social proof**: quantified achievements, client names
- **Published work**: blog posts, open-source contributions, talks, articles
- **Any metrics**: user counts, revenue impact, performance improvements, awards

**Portfolio synthesis rules:**
- Portfolio descriptions are usually richer and more results-oriented than GitHub READMEs — always prefer portfolio text.
- If the portfolio has a "Featured Projects" section, prioritize those in the resume.
- Extract quantified outcomes verbatim (e.g., "reduced load time by 60%", "10k monthly users") — use directly as achievement bullets.
- Include the portfolio URL prominently in the resume header.

If `web_fetch` fails (private site or auth wall), ask the user to paste the key project descriptions, metrics, and bio text manually.

---

## Step 3: Fetch GitHub Data

```
https://api.github.com/users/{username}
https://api.github.com/users/{username}/repos?sort=stars&per_page=10
```

Extract: full name, bio, location, blog URL, top 5 repos by stars (name, description, language, URL), top languages aggregated, total public repos and followers.

If API is unavailable: `site:github.com/{username}` via web search.

Cross-reference with portfolio: elevate any repo featured on the portfolio site in the Projects section.

---

## Step 4: Fetch LeetCode Data (if provided)

```
https://leetcode-stats-api.herokuapp.com/{username}
```

Extract: total solved with Easy/Medium/Hard breakdown, global ranking, acceptance rate, contest rating. If no data, ask to confirm or skip.

---

## Step 5: Fetch Figma Data (if UI/UX role)

Search `figma.com/@{username}` or `site:figma.com {username}`. Extract: public files, likes/followers, featured project names. Cross-reference with portfolio descriptions.

---

## Step 6: Parse LinkedIn Data

Extract: contact info, Summary/About, Work Experience (company, title, dates, bullets), Education (degree, institution, year, GPA if ≥3.5), Skills, Certifications, Honors/Awards, and any Recommendations (mine for quantified praise to use as bullet evidence).

---

## Step 7: ATS Keyword Extraction and Mapping

If a job description was provided:

1. Extract the top 15–20 keywords: required skills, tools, technologies, role verbs ("architected", "deployed", "led"), must-have phrases ("CI/CD", "cross-functional", "stakeholder management").
2. Map each to the resume section where it fits most naturally (Summary, Skills, Experience bullets, Projects).
3. Ensure every hard-required keyword appears at least once. Flag any that cannot be included honestly — never fabricate.
4. Use exact JD phrasing where possible (e.g., "React.js" not "React", "TypeScript" not "TS").

If no JD: write a strong general-purpose resume for the target role using common industry keywords extracted from the user's own profile data.

---

## Step 8: Synthesize Resume Content

| Section | Primary Sources |
|---|---|
| Header | User input + GitHub + Portfolio URL + Figma |
| Summary / Objective | Portfolio bio + LinkedIn About + JD keywords |
| Work Experience | LinkedIn (enhanced with portfolio outcomes) |
| Education | LinkedIn |
| Skills & Tools | LinkedIn + GitHub languages + Portfolio stack + Figma tools |
| Projects | Portfolio featured + GitHub top repos + Figma files |
| Competitive Programming | LeetCode stats (if provided) |
| Certifications | LinkedIn |

**Synthesis rules:**
- Prefer LinkedIn name over GitHub display name.
- Portfolio descriptions take priority over GitHub auto-generated content.
- Write the Summary yourself — 2–3 sentences, target role + JD keywords + the single most impressive data point from the user's profile.
- **Quantify everything available**: "★ 142 GitHub stars", "10k MAU", "Reduced bundle size by 40%", "Led 6-engineer team". Use numbers directly from portfolio/LinkedIn.
- Start every Experience and Project bullet with a strong action verb: Led, Built, Designed, Optimized, Shipped, Reduced, Increased, Architected, Launched, Automated.
- Each Experience role: 3–5 bullets minimum, at least 2 quantified achievements (not just responsibilities).
- Ban all filler: "Responsible for", "Worked on", "Helped with" → replace with direct ownership language.

---

## Step 9: Generate LaTeX Source — 2-Column 1-Page Layout

**Layout structure:**
- **Full-width header**: name (large, bold), target role/title, contact info row (email · phone · location · GitHub · LinkedIn · Portfolio · Figma)
- **Left column (33%)**: Summary, Skills, Tools, Education, Certifications, LeetCode, Languages
- **Right column (67%)**: Work Experience, Projects

---

### Color Palettes — Choose Based on Selected Style

Apply the chosen palette's exact hex values throughout. These are the four palettes most correlated with shortlisting across FAANG, top startups, consulting, and design companies:

#### `navy-gold` — The Universal Shortlister
Used by candidates at Google, McKinsey, Goldman Sachs, Microsoft. Professional authority with just enough warmth to stand out.
```latex
\definecolor{accent}{HTML}{1B2A4A}      % Deep navy — headers, name, section rules
\definecolor{highlight}{HTML}{C9A84C}   % Warm gold — company names, icons, links
\definecolor{bodytext}{HTML}{2D2D2D}    % Near-black — body text
\definecolor{subtle}{HTML}{6B7280}      % Cool gray — dates, secondary info
\definecolor{colbg}{HTML}{F4F6F9}       % Ice blue-white — left column background
```

#### `slate-teal` — The Startup Favorite
Popular at Stripe, Figma, Notion, Airbnb. Sophisticated and modern without being loud.
```latex
\definecolor{accent}{HTML}{1E293B}      % Charcoal slate — headers, name
\definecolor{highlight}{HTML}{0D9488}   % Deep teal — company names, icons, links
\definecolor{bodytext}{HTML}{1E293B}    % Slate — body text
\definecolor{subtle}{HTML}{64748B}      % Muted slate — dates, secondary info
\definecolor{colbg}{HTML}{F0FDFA}       % Teal tint — left column background
```

#### `midnight-coral` — The Creative/Product Pick
Shortlisted at Meta, Pinterest, Spotify, Canva, design agencies. Warm contrast reads as confident and human.
```latex
\definecolor{accent}{HTML}{111827}      % Near-black — headers, name
\definecolor{highlight}{HTML}{E85D4A}   % Warm coral — company names, icons, links
\definecolor{bodytext}{HTML}{1F2937}    % Dark gray — body text
\definecolor{subtle}{HTML}{6B7280}      % Medium gray — dates, secondary info
\definecolor{colbg}{HTML}{FFF7F6}       % Blush white — left column background
```

#### `classic-mono` — Maximum ATS Safety
Use for banking, law, government, or any conservative industry. Zero color risk, zero parse risk.
```latex
\definecolor{accent}{HTML}{111111}      % Near-black — headers, name
\definecolor{highlight}{HTML}{333333}   % Dark gray — company names, links
\definecolor{bodytext}{HTML}{222222}    % Body text
\definecolor{subtle}{HTML}{777777}      % Dates, secondary info
\definecolor{colbg}{HTML}{F5F5F5}       % Light gray — left column background
```

---

### Typography

```latex
\usepackage[T1]{fontenc}
\usepackage{charter}          % Elegant serif — best overall readability and recruiter appeal
% Fallback: \usepackage{lmodern}
```

- Name: `\fontsize{22pt}{26pt}\selectfont\bfseries` in `accent` color
- Role/title under name: `\fontsize{10pt}{12pt}\selectfont\color{subtle}`
- Section headers: `\fontsize{9pt}{11pt}\selectfont\scshape\color{accent}` with a 0.5pt `highlight`-colored rule underneath
- Body: 10pt, `bodytext` color
- Company/org names: `\bfseries\color{highlight}`
- Dates: `\color{subtle}\small`, right-aligned

---

### LaTeX Packages

```latex
\usepackage[margin=0.5in, top=0.45in]{geometry}
\usepackage{paracol}
\usepackage[T1]{fontenc}
\usepackage{charter}
\usepackage{hyperref}
\usepackage{enumitem}
\usepackage{xcolor}
\usepackage{titlesec}
\usepackage{fontawesome5}     % skip if unavailable
\usepackage{microtype}        % improves text density and justification
```

Hyperref config:
```latex
\hypersetup{
  colorlinks=true,
  urlcolor=highlight,
  linkcolor=highlight,
  pdfborder={0 0 0}
}
```

---

### Layout Details

**Left column background:**
```latex
\backgroundcolor{c[0]}(0pt,0pt)(0.5\paperwidth,\paperheight){colbg}
% or use \columncolor{colbg} if backgroundcolor is unavailable
```

**Section header command:**
```latex
\newcommand{\sectionheader}[1]{%
  \vspace{6pt}
  {\fontsize{9pt}{11pt}\selectfont\scshape\color{accent} #1}
  \vspace{1pt}
  {\color{highlight}\hrule height 0.5pt}
  \vspace{4pt}
}
```

**Experience entry:**
```latex
\newcommand{\expentry}[4]{%       {Title}{Company}{Location}{Dates}
  {\bfseries #1} \hfill {\color{subtle}\small #4} \\
  {\color{highlight}\bfseries #2} \hspace{2pt} {\color{subtle}\small #3}
}
```

**Skill tags** (ATS-safe, plain inline text):
```latex
% Use simple text with middot separators — NO fboxes, NO tcolorbox
Python \textbullet{} TypeScript \textbullet{} React.js \textbullet{} AWS
```

**Projects** (2-across minipage grid):
```latex
\begin{minipage}[t]{0.48\linewidth}
  {\bfseries\color{accent} Project Name} \\
  {\color{subtle}\small Tech Stack} \\
  One-line outcome or metric.
\end{minipage}
\hfill
\begin{minipage}[t]{0.48\linewidth}
  ...
\end{minipage}
```

---

### ATS Safety Rules (Non-Negotiable)

- Never use `tabular` or `table` for layout — use `paracol` and `minipage` only.
- Never use `\fbox`, `tcolorbox`, or text boxes for skills — plain inline text only.
- All text must be selectable PDF text, never rasterized.
- Section heading names must be conventional: "Work Experience", "Education", "Skills", "Projects", "Certifications".
- Keep `colorlinks=true` — links must be clickable.
- Escape all special characters: `&`→`\&`, `%`→`\%`, `#`→`\#`, `_`→`\_`

Save as `resume_<username>.tex`.

---

## Step 10: Compile to PDF

```bash
cd /home/claude
pdflatex -interaction=nonstopmode resume_<username>.tex
pdflatex -interaction=nonstopmode resume_<username>.tex   # second pass for links/refs
```

If `pdflatex` unavailable, try `xelatex`. On failure: read `.log`, fix, retry up to 3 times. If still failing, deliver `.tex` and suggest Overleaf.com.

---

## Step 11: Deliver to User

```bash
cp resume_<username>.tex /mnt/user-data/outputs/
cp resume_<username>.pdf /mnt/user-data/outputs/
```

Use `present_files` to share both. Summary should cover: which sources were used, ATS keywords incorporated (if JD was provided), any data gaps, and a note that the `.tex` file can be customized further at Overleaf.com.

---

## Notes & Edge Cases

- **Missing LinkedIn**: Proceed with GitHub + Portfolio + LeetCode. Omit Work Experience, Education, Certifications; flag gaps to user.
- **Private GitHub**: Ask user to paste top 3–5 projects manually (name, description, stack, link).
- **No portfolio URL**: Proceed without. Recommend creating one (GitHub Pages, Vercel, Notion) and adding the link to the header.
- **Portfolio behind auth**: Ask user to paste bio, project descriptions, and metrics directly.
- **No LeetCode**: Skip Competitive Programming entirely — no placeholder.
- **UI/UX role without Figma**: Include design tools in Skills from LinkedIn/portfolio; leave Figma header link blank.
- **No job description**: Write a strong general summary using common industry keywords from the user's own data.
- **1-page overflow**: Trim in this order — cut experience bullets to 3 per role → remove LeetCode section → remove Certifications → cut Projects to top 3.
- **Academic style**: Single-column layout, promote Education and Publications to the top of the right column.
- **Multiple target roles**: Note that a role-specific resume always outperforms a generic one. Offer separate tailored versions.