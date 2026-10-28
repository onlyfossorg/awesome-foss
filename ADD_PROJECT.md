# How to Add Your Project

> Step-by-step guide to showcase your college open-source project on ONLY FOSS ORG.

Adding your project takes less than 2 minutes. You only need to add a single file under `projects/`:
- **YAML format (Recommended for humans):** `projects/<your-project-slug>.yml`
- **JSON format:** `projects/<your-project-slug>.json`

You can use whichever format you find easier!

---

## Prerequisite Checklist

Before submitting, **your project's own GitHub repository** (the link you will submit) must include these 3 files at its root:

| File | Purpose |
| ---- | ------- |
| `README.md` | Clear description of what the project does, how to set it up, and how to run it |
| `CONTRIBUTING.md` | Guidelines on how others can contribute to your project |
| `LICENSE` / `LICENSE.md` | An open-source license (e.g., MIT, Apache 2.0, GPL) |

> **Important:** Do **NOT** clone, copy, or paste your project's source code, `README.md`, or `CONTRIBUTING.md` into this repository. You only submit a single metadata file (`projects/<your-slug>.yml` or `projects/<your-slug>.json`).

---

## Choose How to Submit

### Option 1: Via GitHub Web (Easiest - No Git or Terminal Required)

1. **Fork the repo**: Click the **Fork** button at the top-right of [onlyfossorg/awesome-foss](https://github.com/onlyfossorg/awesome-foss).
2. **Create your project file**:
   - In your fork, navigate into the [`projects/`](projects/) folder.
   - Click **Add file** -> **Create new file**.
   - In the name box, type `<your-project-slug>.yml` (example: `lanview-cli.yml`) or `<your-project-slug>.json`.
3. **Fill in your details**:
   - Paste the [YAML Template](#format-1-yaml-template-recommended) or [JSON Template](#format-2-json-template) below and fill in your project's details.
4. **Commit & Open PR**:
   - Click **Commit changes...** (commit message: `Add project: <Your Project Name>`).
   - Go to the **Pull requests** tab and click **New pull request** -> **Create pull request**.

Done! Our automated GitHub CI will validate your submission.

---

### Option 2: Via Terminal / CLI (For Developers)

```bash
# 1. Clone your fork and create a branch
git checkout -b add-<your-project-slug>

# 2. Create your project file in projects/
# (e.g., projects/my-app.yml or projects/my-app.json) using the template below

# 3. Validate locally
node dev/scripts/build-projects.js

# 4. Commit and push
git add projects/<your-project-slug>.*
git commit -m "Add project: <Your Project Name>"
git push -u origin add-<your-project-slug>

# 5. Open a Pull Request via GitHub or GitHub CLI
gh pr create --title "Add project: <Your Project Name>"
```

---

## Format 1: YAML Template

Create `projects/<your-project-slug>.yml`:

```yaml
slug: your-project-slug
name: Your Project Name
tagline: One punchy line describing what your project does (max 150 chars).
description: >
  A clear, descriptive summary of the project, features,
  and target users (10-500 characters).
status: active
difficulty: beginner

tech_stack:
  - React
  - Node.js
  - Tailwind CSS

github_repo: https://github.com/your-username/your-project-repo

maintainers:
  - name: Your Name
    contact: https://github.com/your-username

looking_for_contributors: true

domain:
  - Web
  - AI/ML
  - GenAI
  - Tools
  - IoT/Embedded
  - Blockchain
  - Mobile
  - Cybersecurity
  - Cloud/DevOps
  - Data/Analytics
  - Game Dev
  - Systems
```

---

## Format 2: JSON Template

Create `projects/<your-project-slug>.json`:

```json
{
  "slug": "your-project-slug",
  "name": "Your Project Name",
  "tagline": "One punchy line describing what your project does (max 150 chars).",
  "description": "A clear, descriptive summary of the project, features, and target users (10-500 characters).",
  "status": "active",
  "difficulty": "beginner",
  "tech_stack": [
    "React",
    "Node.js",
    "Tailwind CSS"
  ],
  "github_repo": "https://github.com/your-username/your-project-repo",
  "maintainers": [
    {
      "name": "Your Name",
      "contact": "https://github.com/your-username"
    }
  ],
  "looking_for_contributors": true,
  "domain": [
    "Web", "AI/ML", "GenAI", "Tools", "IoT/Embedded", "Blockchain", "Mobile", "Cybersecurity", "Cloud/DevOps", "Data/Analytics", "Game Dev", "Systems"
  ]
}
```

> **Note on backward compatibility:** If you prefer subfolders (`projects/<slug>/project.yml` or `projects/<slug>/project.json`), both structures are supported.

---

## Available Domain Categories

Pick one or more categories that describe your project:

- `"Web"` — Full-stack web applications, frontends, APIs, backends
- `"AI/ML"` — Machine learning, computer vision, data modeling
- `"GenAI"` — LLMs, generative AI tools, AI agents
- `"Tools"` — Developer CLI tools, desktop utilities, productivity tools
- `"Mobile"` — Android, iOS, Flutter, React Native applications
- `"Cybersecurity"` — Security tools, network scanners, encryption utilities
- `"Cloud/DevOps"` — Containers, infrastructure, server automation, CI/CD
- `"Data/Analytics"` — Data pipelines, scrapers, analytics dashboards
- `"Game Dev"` — 2D/3D games, game engines, interactive simulations
- `"IoT/Embedded"` — Hardware integrations, microcontrollers, robotics
- `"Blockchain"` — Smart contracts, dApps, Web3 protocols
- `"Systems"` — Low-level systems, compilers, OS utilities, kernels

---

## Slug Rules

Your `slug` is the unique identifier for your project.

- Must be **lowercase kebab-case** (letters, numbers, hyphens only).
- Must match your filename: `projects/<slug>.yml` or `projects/<slug>.json`.
- [✅] `lanview-cli` -> `projects/lanview-cli.yml` or `projects/lanview-cli.json`
- [✅] `smart-irrigation` -> `projects/smart-irrigation.yml` or `projects/smart-irrigation.json`
- [❌] `LanView_CLI` (no capitals or underscores)
- [❌] `smart irrigation` (no spaces)

---

## Support the Community

- Star ⭐ [awesome-foss](https://github.com/onlyfossorg/awesome-foss) to help more student developers discover it.
- Follow [ONLY FOSS ORG](https://github.com/onlyfossorg) on GitHub.
- Have questions? Open a [Discussion](https://github.com/onlyfossorg/awesome-foss/discussions) or [Issue](https://github.com/onlyfossorg/awesome-foss/issues).
