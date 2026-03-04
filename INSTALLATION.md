

## How to Install the Resume Builder Skill in Claude

### What You Need Before Starting

A **Claude Pro, Team, or Enterprise** account at [claude.ai](https://claude.ai). The Skills feature requires access to **Projects**, which is available on paid plans. A free account will not work.

---

### Step 1 — Download the Skill File

Go to your GitHub repository:
**https://github.com/Itinerant18/Claude-skills-resume-builder**

Navigate to `skill/resume-builder/SKILL.md`. Click the file, then click the **Raw** button in the top-right corner. Right-click anywhere on the page and choose **Save As**, saving the file as `SKILL.md` on your computer.

Alternatively, download the entire repository as a ZIP by clicking **Code → Download ZIP**, then extract it and locate `skill/resume-builder/SKILL.md` inside.

---

### Step 2 — Create a Project in Claude

Open [claude.ai](https://claude.ai) and click **Projects** in the left sidebar. Click **New Project** and give it a name — something like `Resume Builder` works well. A Project is simply a persistent workspace that keeps the skill's instructions in context across all your conversations.

---

### Step 3 — Upload the Skill File to Your Project

Inside your new Project, look for the **"Add content"** or **"Set instructions"** option (the exact label depends on your Claude interface version). Upload the `SKILL.md` file you downloaded in Step 1, or open the file in a text editor, select all the text, and paste it into the Project instructions field.

Once saved, Claude will have the full resume-building capability available in every conversation you start within that Project.

---

### Step 4 — Start Building Your Resume

Open a new chat inside the Project. Claude will now automatically recognize resume-building requests. You can start with something like:

> *"Build my resume from my GitHub profile and LinkedIn. I'm targeting a Senior Backend Engineer role at Stripe. Use the navy-gold style."*

Claude will respond with a single message asking for everything it needs — your GitHub username, LinkedIn text, portfolio URL, contact details, and optionally a job description for ATS keyword targeting. You provide everything in one reply, and Claude handles the rest.

---

### What Claude Will Deliver

Once it has your information, Claude generates and compiles two files: a **PDF** ready to submit to employers, and a **`.tex` LaTeX source file** you can open at [Overleaf.com](https://overleaf.com) if you want to make manual adjustments to layout or wording.

---

### Choosing a Color Style

When Claude asks for your preferred style, the four options are:

| Style | Best For |
|---|---|
| `navy-gold` | Tech, finance, consulting, product roles — the most broadly shortlisted palette |
| `slate-teal` | Startups and design-forward companies (Stripe, Figma, Airbnb) |
| `midnight-coral` | Creative, product, and design roles (Meta, Spotify, Canva) |
| `classic-mono` | Banking, law, government, and other conservative industries |

If you are unsure, choose `navy-gold` — it performs well across the widest range of companies and roles.

---

### Troubleshooting

**"Claude doesn't seem to understand it's a resume skill"** — Make sure you started the conversation inside the Project where you uploaded the skill, not in a regular Claude chat.

**"I don't have a Projects option"** — Projects are only available on Claude Pro and above. Upgrade your plan at `claude.ai/settings`.

**"The PDF failed to compile"** — Claude will automatically retry up to three times. If it still fails, it will deliver the `.tex` file instead, which you can compile for free at [Overleaf.com](https://overleaf.com) by creating a free account and uploading the file.

