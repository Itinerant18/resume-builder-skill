---
name: resume-builder
description: "Build a professional, ATS-optimized LaTeX + PDF resume from any combination of inputs — GitHub, LinkedIn, LeetCode, Figma, portfolio website, an uploaded old resume, or just a self-description. Works for ALL sectors including tech, BPO, call center, customer service, banking, operations, healthcare, sales, and HR. Use this skill whenever a user wants to create or generate a resume or CV. Trigger on: build my resume, make a CV, I only have LinkedIn, resume from my old resume, I will describe myself, resume for BPO job, call center resume, customer service resume, help me get shortlisted, optimize for ATS. Even if the user has no GitHub/portfolio/Figma — just LinkedIn, an old resume, or only a self-description — still use this skill and proceed with whatever is available."
---
 
# Resume Builder Skill
 
Builds a polished, ATS-optimized, 2-column 1-page resume in both `.tex` (LaTeX source) and `.pdf` formats. Works for **any sector** — tech, BPO/call center, customer service, banking, operations, sales, HR, healthcare, and more. Accepts any combination of inputs: GitHub, LinkedIn, LeetCode, Figma, portfolio website, an uploaded old resume (PDF/DOCX), or just the user's own self-description. The final output is engineered to pass ATS screening and catch a recruiter's eye within 6 seconds.
 
> **Minimum viable input**: Even if the user has only LinkedIn + a self-description, this skill can still produce a strong, tailored resume. Never block on missing inputs.
 
---
 
## Step 1: Gather Inputs
 
Ask the user for everything **in a single message** — do not ask one by one. Frame it as "tell me what you have" rather than a checklist of requirements. All fields are optional except personal contact info.
 
**Profile sources (use whatever the user has — none are required):**
1. **GitHub username or URL** *(for tech/developer roles)*
2. **LinkedIn export text** — paste About, Experience, Education, Skills, Certifications
3. **Old resume file** — upload PDF or DOCX, or paste the text directly
4. **Self-description** — "Just tell me about yourself": current/past roles, key skills, achievements, years of experience, notable moments
5. **Portfolio / personal website URL** *(if any — Notion, Behance, GitHub Pages, etc.)*
6. **LeetCode username** *(optional, for competitive programmers)*
7. **Figma username** *(optional, for UI/UX designers)*
 
**Personal contact info (required):**
8. Full name, email, phone, location/city
 
**Role targeting:**
9. **Target job title** — e.g., "BPO Team Lead", "Customer Service Representative", "Senior Frontend Engineer", "Operations Manager"
10. **Target sector / industry** — e.g., BPO, tech, banking, healthcare, sales, HR *(helps apply the right keywords and tone)*
11. **Target company** *(optional)*
12. **Job description** *(optional but strongly recommended)* — paste full JD for ATS keyword optimization
13. **Resume style** — ask them to choose:
    - `navy-gold` — Deep navy + gold accent. Professional authority. Works for tech, finance, consulting, BPO management, product.
    - `slate-teal` — Charcoal + teal. Startup-forward and modern.
    - `midnight-coral` — Near-black + coral. Creative and product roles.
    - `classic-mono` — Pure black and white. Maximum ATS safety. Best for banking, law, government, conservative BPO clients.
 
**If the user says "I don't have GitHub" / "I only have LinkedIn" / "I'll just describe myself":** That's completely fine — acknowledge this positively and proceed. Do not ask for GitHub or Figma again.
 
---
 
## Step 2: Parse Old Resume (if provided)
 
If the user uploaded or pasted an old resume, extract all structured data from it:
 
- **Contact info** (name, email, phone, location)
- **Work Experience**: company, title, dates, bullet points
- **Education**: degree, institution, year, GPA
- **Skills**: technical tools, soft skills, languages
- **Certifications / Training**
- **Achievements or Awards**
 
Use this as the foundational data layer — then enrich with anything from LinkedIn, self-description, or other sources. Old resume data is often the most complete single source for non-tech users, so treat it as primary if GitHub/portfolio are absent.
 
If uploaded as PDF/DOCX, read it using bash tools. If pasted as text, parse directly.
 
---
 
## Step 2b: Parse Self-Description (if provided)
 
If the user describes themselves in free text (e.g., "I've worked at XYZ BPO for 3 years handling customer escalations, trained 10 new agents, and was promoted to team lead last year"), extract structured resume content:
 
- Map free-text claims to resume bullets: "trained 10 new agents" → "Onboarded and trained 10 new customer service agents"
- Identify role titles, company names, dates, and responsibilities
- Convert "I did X" language into strong third-person action verb bullets: "Managed", "Led", "Handled", "Resolved", "Achieved"
- Ask one clarifying follow-up question only if a critical piece is missing (e.g., company name, dates, or metrics) — keep it brief and bundle multiple gaps into one ask
 
---
 
## Step 3: Fetch and Parse Portfolio Website (if provided)
 
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
 
## Step 4: Fetch GitHub Data (if provided)
 
```
https://api.github.com/users/{username}
https://api.github.com/users/{username}/repos?sort=stars&per_page=10
```
 
Extract: full name, bio, location, blog URL, top 5 repos by stars (name, description, language, URL), top languages aggregated, total public repos and followers.
 
If API is unavailable: `site:github.com/{username}` via web search.
 
Cross-reference with portfolio: elevate any repo featured on the portfolio site in the Projects section.
 
---
 
## Step 5: Fetch LeetCode Data (if provided)
 
```
https://leetcode-stats-api.herokuapp.com/{username}
```
 
Extract: total solved with Easy/Medium/Hard breakdown, global ranking, acceptance rate, contest rating. If no data, ask to confirm or skip.
 
---
 
## Step 6: Fetch Figma Data (if UI/UX role and provided)
 
Search `figma.com/@{username}` or `site:figma.com {username}`. Extract: public files, likes/followers, featured project names. Cross-reference with portfolio descriptions.
 
---
 
## Step 7: Parse LinkedIn Data (if provided)
 
Extract: contact info, Summary/About, Work Experience (company, title, dates, bullets), Education (degree, institution, year, GPA if ≥3.5), Skills, Certifications, Honors/Awards, and any Recommendations (mine for quantified praise to use as bullet evidence).
 
---
 
## Step 8: ATS Keyword Extraction and Mapping
 
If a job description was provided:
 
1. Extract the top 15–20 keywords: required skills, tools, technologies, role verbs ("architected", "deployed", "led", "handled", "resolved", "managed"), must-have phrases.
2. Map each to the resume section where it fits most naturally (Summary, Skills, Experience bullets, Projects).
3. Ensure every hard-required keyword appears at least once. Flag any that cannot be included honestly — never fabricate.
4. Use exact JD phrasing where possible.
 
**BPO / Customer Service / Operations sector keywords to watch for and include:**
- Customer Satisfaction (CSAT), Net Promoter Score (NPS), First Call Resolution (FCR), Average Handle Time (AHT)
- Escalation management, SLA adherence, quality assurance (QA), call monitoring
- CRM tools: Salesforce, Zendesk, Freshdesk, Avaya, Genesys
- Inbound/outbound, voice/non-voice, chat support, email support
- Workforce management, scheduling, attrition rate, shrinkage
- KPI management, performance coaching, floor walking, floor support
- Upselling, cross-selling, collections, technical support, back-office operations
 
If no JD: write a strong general-purpose resume for the target role using common industry keywords extracted from the user's own profile data.
 
---
 
## Step 9: Synthesize Resume Content
 
| Section | Primary Sources |
|---|---|
| Header | User input + GitHub + Portfolio URL + Figma |
| Summary / Objective | Self-description + Portfolio bio + LinkedIn About + Old resume + JD keywords |
| Work Experience | LinkedIn + Old resume + Self-description (enhanced with outcomes) |
| Education | LinkedIn + Old resume + Self-description |
| Skills & Tools | LinkedIn + GitHub languages + Portfolio stack + Figma tools + Self-described tools |
| Projects | Portfolio featured + GitHub top repos + Self-described projects |
| Certifications | LinkedIn + Old resume + Self-description |
| Competitive Programming | LeetCode stats (if provided) |
 
**Synthesis rules:**
- Work with whatever sources are available — never leave a section empty just because one source is missing.
- Self-described achievements are valid — convert them faithfully into polished bullet language.
- Write the Summary yourself — 2–3 sentences: target role + key differentiator + most impressive claim from any source.
- **Quantify everything available**: "Handled 80+ calls/day", "Maintained 95% CSAT", "Trained 10 agents", "★ 142 GitHub stars", "10k MAU".
- Start every Experience and Project bullet with a strong action verb: Led, Built, Handled, Resolved, Managed, Trained, Optimized, Launched, Achieved, Coordinated.
- Each Experience role: 3–5 bullets minimum, at least 2 quantified achievements (not just responsibilities).
- Ban all filler: "Responsible for", "Worked on", "Helped with" → replace with direct ownership language.
 
**BPO / Customer Service tone rules:**
- Emphasize soft skills with evidence: "Maintained top-quartile CSAT scores for 6 consecutive quarters"
- Use industry-standard metrics as bullet anchors: AHT, FCR, CSAT, NPS, SLA
- For team lead / supervisory roles: highlight headcount managed, coaching outcomes, and attrition impact
- For individual contributor roles: highlight volume (calls/tickets/chats per day), accuracy, and satisfaction scores
 
---
 
## Step 10: Generate LaTeX Source — 2-Column 1-Page Layout
 
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
 
## Step 11: Compile to PDF
 
```bash
cd /home/claude
pdflatex -interaction=nonstopmode resume_<username>.tex
pdflatex -interaction=nonstopmode resume_<username>.tex   # second pass for links/refs
```
 
If `pdflatex` unavailable, try `xelatex`. On failure: read `.log`, fix, retry up to 3 times. If still failing, deliver `.tex` and suggest Overleaf.com.
 
---
 
## Step 12: Deliver to User
 
```bash
cp resume_<username>.tex /mnt/user-data/outputs/
cp resume_<username>.pdf /mnt/user-data/outputs/
```
 
Use `present_files` to share both. Summary should cover: which sources were used, ATS keywords incorporated (if JD was provided), any data gaps, and a note that the `.tex` file can be customized further at Overleaf.com.
 
---
 
## Notes & Edge Cases
 
- **No GitHub / No Figma / No Portfolio**: Completely fine — proceed with LinkedIn + old resume + self-description. Do NOT prompt for these again after the user says they don't have them.
- **Only self-description, no other sources**: Ask 2–3 targeted follow-up questions (company names, dates, key metrics) in a single message, then build the resume from the answers.
- **Old resume only (no LinkedIn, no GitHub)**: Parse it fully, ask for target role and any updates, then produce an improved version.
- **LinkedIn only**: Proceed with LinkedIn data. Ask for target role and any highlights not on LinkedIn.
- **Missing LinkedIn**: Proceed with GitHub + Portfolio + old resume + self-description. Flag gaps to user.
- **Private GitHub**: Ask user to paste top 3–5 projects manually.
- **No portfolio URL**: Proceed without. Recommend creating one and adding to the header.
- **No LeetCode**: Skip Competitive Programming entirely — no placeholder.
- **UI/UX role without Figma**: Include design tools from LinkedIn/portfolio in Skills section.
- **No job description**: Write a strong general summary using common industry keywords from the user's sector and own data.
- **BPO / Customer Service role**: See Step 8 for sector-specific keywords and Step 9 for tone rules. Emphasize CSAT, AHT, FCR, and volume metrics. Use `classic-mono` or `navy-gold` style for conservative BPO clients.
- **1-page overflow**: Trim in order — cut experience bullets to 3 per role → remove LeetCode section → remove Certifications → cut Projects to top 3.
- **Academic style**: Single-column layout, promote Education and Publications to top of right column.
- **Multiple target roles**: Note that a role-specific resume always outperforms a generic one. Offer separate tailored versions.
