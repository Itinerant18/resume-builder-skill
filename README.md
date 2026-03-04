# 🧠 Resume Builder — Claude Skill

> A Claude skill that builds ATS-optimized, recruiter-ready resumes by pulling data from your GitHub, LinkedIn, LeetCode, Figma, and personal portfolio — and generating a polished PDF in seconds.

---

## ✨ What This Skill Does

Once installed, this skill lets you say things like **"build my resume from my GitHub and LinkedIn"** directly to Claude, and it will:

1. Fetch your GitHub profile and top repositories automatically
2. Pull project details, metrics, and bio from your portfolio website
3. Parse your pasted LinkedIn data (experience, education, skills)
4. Optionally pull LeetCode stats and Figma community files
5. Extract ATS keywords from a job description you paste
6. Generate a 2-column, 1-page LaTeX resume with a professional color palette
7. Compile and deliver both a `.tex` source file and a ready-to-submit `.pdf`

The output is designed to pass Applicant Tracking Systems (ATS) and catch a recruiter's attention within 6 seconds.

---

## 🎨 Color Palettes

Four recruiter-tested palettes are included. You choose one when starting:

| Style | Colors | Best For |
|---|---|---|
| `navy-gold` | Deep navy + warm gold | Tech, finance, consulting, product (most universally shortlisted) |
| `slate-teal` | Charcoal slate + deep teal | Startups, design-forward companies (Stripe, Figma, Airbnb) |
| `midnight-coral` | Near-black + warm coral | Creative, product, and design roles (Meta, Spotify, Canva) |
| `classic-mono` | Black and white only | Banking, law, government, conservative industries |

---

## 📋 Prerequisites

Before using this skill you need:

- A **Claude Pro, Team, or Enterprise** account at [claude.ai](https://claude.ai) — Skills require the Projects feature
- Your **GitHub username** (public profile)
- Your **LinkedIn text** — copy-paste from your LinkedIn About, Experience, Education, Skills sections
- Optionally: a portfolio/personal website URL, LeetCode username, Figma username
- Optionally: a job description to paste for ATS keyword targeting

No API keys, no local installations, no LaTeX setup required. Everything runs inside Claude.

---

## 🚀 Installation

### Step 1 — Download the skill file

Download [`skill/resume-builder/SKILL.md`](./skill/resume-builder/SKILL.md) from this repository. You can do this by:

- Clicking the file → clicking **Raw** → saving the page as `SKILL.md`
- Or cloning the repo: `git clone https://github.com/YOUR_USERNAME/resume-builder-skill.git`

### Step 2 — Open Claude and go to a Project

Navigate to [claude.ai](https://claude.ai), open an existing **Project** or create a new one (e.g., "Resume Builder").

### Step 3 — Upload the skill

Inside the Project, look for **"Add content"** or **"Project instructions"** and upload (or paste the contents of) `SKILL.md`.

> **Tip:** Name the project something descriptive like "My Resume Builder" so Claude always has the skill in context when you open that project.

### Step 4 — Start a conversation

Open a new chat inside the project and say something like:

```
Build my resume from my GitHub and LinkedIn. I'm targeting a Senior Backend Engineer role at Stripe.
```

Claude will ask you for everything it needs in a single message.

---

## 💬 Example Prompts

```
Build my resume from my GitHub profile johndoe and the LinkedIn text below.
Target role: Product Manager at Google. Use navy-gold style.
```

```
Create an ATS-optimized CV from my GitHub (johndoe), my portfolio at johndoe.dev,
and the job description I'll paste. I'm applying to Spotify.
```

```
Make a resume for me. I'm a UI/UX designer, here's my Figma username and LinkedIn.
Help me get shortlisted at a design agency.
```

```
Generate a resume from my profiles. GitHub: johndoe, LeetCode: johndoe.
Targeting software engineering roles at FAANG. Use slate-teal style.
```

---

## 📁 Repository Structure

```
resume-builder-skill/
├── README.md                          ← You are here
├── skill/
│   └── resume-builder/
│       └── SKILL.md                   ← The skill file to upload to Claude
├── examples/
│   ├── sample-navy-gold.png           ← Preview of navy-gold palette output
│   ├── sample-slate-teal.png          ← Preview of slate-teal palette output
│   └── what-to-paste-from-linkedin.md ← Guide for exporting your LinkedIn data
└── CONTRIBUTING.md                    ← How to improve or fork this skill
```

---

## 📄 What You'll Receive

After running the skill, Claude delivers two files:

- **`resume_<username>.pdf`** — The compiled, print-ready resume. Submit this to employers.
- **`resume_<username>.tex`** — The LaTeX source. Open at [Overleaf.com](https://overleaf.com) if you want to manually adjust spacing, wording, or layout.

---

## 🔧 Customization

You can modify `SKILL.md` to change default behaviors. Some useful tweaks:

**Change the default palette** — Find `navy-gold` in Step 1 and reorder the list, or hardcode a default.

**Add a new section** — Add a row to the synthesis table in Step 8 and describe where Claude should pull data from.

**Adjust layout proportions** — The left/right column split is 33/67. You can change this in the `paracol` setup inside Step 9.

**Add a new color palette** — Follow the exact format in the Color Palettes section: define five colors (`accent`, `highlight`, `bodytext`, `subtle`, `colbg`) and give the palette a name and description.

---

## 🤝 Contributing

Contributions are welcome. Please read [`CONTRIBUTING.md`](./CONTRIBUTING.md) before submitting a pull request.

Ideas for contributions: new color palettes, support for additional profile sources (Dribbble, Google Scholar, Dev.to), a two-page academic variant, or translations of the instruction prompts.

---

## 📜 License

MIT License — free to use, modify, and distribute. See [`LICENSE`](./LICENSE) for details.

---

## ⭐ Support

If this skill helped you land an interview or get shortlisted, consider starring the repository — it helps others find it.

For issues or questions, open a [GitHub Issue](../../issues).