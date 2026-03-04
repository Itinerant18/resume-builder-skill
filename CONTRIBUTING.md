# Contributing to Resume Builder Skill

Thank you for your interest in improving this skill. Contributions of all kinds are welcome — new features, bug fixes, new color palettes, better instructions, or additional profile source integrations.

---

## How to Contribute

### Reporting Issues

If the skill produces incorrect LaTeX, fails to compile, misses a data source, or behaves unexpectedly, please open a [GitHub Issue](../../issues) with:

- A description of what happened versus what you expected
- Which profile sources you provided (GitHub, LinkedIn, portfolio, etc.)
- The resume style you selected
- The error or output you received (you can redact personal info)

### Suggesting Improvements

Open an issue with the label `enhancement`. Good candidates include:

- New color palettes (follow the five-color format: `accent`, `highlight`, `bodytext`, `subtle`, `colbg`)
- New profile source integrations (Dribbble, Google Scholar, Dev.to, Behance)
- A two-page academic variant
- Better overflow / 1-page fitting logic
- Language or locale support

### Submitting a Pull Request

1. Fork the repository
2. Create a branch: `git checkout -b feature/your-feature-name`
3. Make your changes to `skill/resume-builder/SKILL.md`
4. Test the skill by uploading your modified `SKILL.md` to a Claude Project and running it against a real or sample profile
5. Commit your changes with a clear message: `git commit -m "Add Dribbble profile source integration"`
6. Push and open a Pull Request against `main`

---

## Skill File Guidelines

When editing `SKILL.md`, please follow these conventions:

- Keep all instructions imperative and unambiguous ("Extract the top 15–20 keywords" not "You might want to extract keywords")
- Every new data source should have its own numbered step following the existing pattern: Fetch → Extract → Cross-reference with portfolio
- Color palettes must define all five color roles: `accent`, `highlight`, `bodytext`, `subtle`, `colbg`
- ATS safety rules in Step 9 are non-negotiable — do not introduce `tabular`, `tcolorbox`, or rasterized elements
- Keep the skill under 500 lines where possible

---

## License

By contributing, you agree that your contributions will be licensed under the MIT License.