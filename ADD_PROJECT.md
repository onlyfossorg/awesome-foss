# How to Add Your Project

> **Step-by-step CLI guide to submit your project to the ONLY FOSS ORG directory of college projects kept alive as open source**

You will add two files under `projects/<slug>/` (`project.json` and `README.md`), then open a pull request.

## Before You Start

Your **project's own GitHub repository** (the one you list in `github_repo`) must already include these files at the repo root:

| File | Purpose |
| ---- | ------- |
| `README.md` | Describes the project, setup, and usage |
| `CONTRIBUTING.md` | Explains how others can contribute |
| `LICENSE.md` | States the open-source license (a root `LICENSE` file is also acceptable) |

Do not open a PR here until those files are present and valid in your project repo. Maintainers will reject submissions that are missing them.

✅ **Checkpoint:** Your project repo has `README.md`, `CONTRIBUTING.md`, and `LICENSE.md` (or `LICENSE`).

---

## Tutorial Overview

### Step 1: Follow the ONLY FOSS ORG Organization

1. Go to the [ONLY FOSS ORG Organization page](https://github.com/onlyfossorg)
2. If you aren't already following, click the **"Follow"** button under the organization name.

✅ **Checkpoint:** You'll stay updated with ONLY FOSS ORG activity!

---

### Step 2: Star the Repository

1. Go to the [awesome-foss repository](https://github.com/onlyfossorg/awesome-foss)
2. If you haven't already, click the **"Star"** button at the top-right of the page.

✅ **Checkpoint:** This helps more people discover the directory!

---

### Step 3: Fork and Clone

With the [GitHub CLI](https://cli.github.com/) installed and authenticated (`gh auth login`):

```bash
gh repo fork onlyfossorg/awesome-foss --clone
cd awesome-foss
```

If you prefer to fork in the browser first, then clone your copy:

```bash
git clone https://github.com/YOUR-USERNAME/awesome-foss.git
cd awesome-foss
```

✅ **Checkpoint:** You have a local clone of your fork.

---

### Step 4: Choose Your Project Slug

Your **slug** is your project's unique identifier. You will use it as the folder name, the `slug` field in `project.json`, and the git branch name.

### Rules:

- ✅ Lowercase only
- ✅ Use hyphens (not spaces or underscores)
- ✅ Descriptive and short

### Examples:

| Valid ✅         | Invalid ❌      |
| ---------------- | --------------- |
| `my-cool-app`    | `mycoolapp`     |
| `ai-chatbot`     | `AI-CHATBOT`    |
| `student-portal` | `StudentPortal` |

💡 **Write down your slug — you'll need it in the next steps!**

---

### Step 5: Create a Branch

Replace `your-project-slug` with your actual slug:

```bash
git checkout -b add-your-project-slug
```

✅ **Checkpoint:** You are on a dedicated branch for this project.

---

### Step 6: Create Your Project Folder & Files

```bash
mkdir -p projects/your-project-slug
```

Create `projects/your-project-slug/project.json` with this template, then fill in your project details:

```json
{
  "slug": "your-project-slug",
  "name": "Your Project Name",
  "tagline": "One line about what it does",
  "description": "A longer description (10-500 characters).",
  "status": "status here (active, dormant, idea)",
  "difficulty": "difficulty here (beginner, intermediate, advanced)",
  "tech_stack": ["React", "Python"],
  "github_repo": "https://github.com/your-project-repo",
  "maintainers": [
    {
      "name": "Your Name",
      "contact": "your@email.com"
    }
  ],
  "looking_for_contributors": true,
  "domain": ["Web", "AI/ML", "GenAI", "Blockchain", "IoT/Embedded"]
}
```

Create `projects/your-project-slug/README.md` with:

- What the project is
- Tech stack
- How to run it

The `slug` in `project.json` must match the folder name.

✅ **Checkpoint:** Your project folder contains both required files.

---

### Step 7: Validate Locally (Recommended)

From the repository root:

```bash
node dev/scripts/build-projects.js
```

This checks `project.json` against the schema and confirms the folder name matches the slug.

✅ **Checkpoint:** The build script completes without errors.

---

### Step 8: Commit and Push

```bash
git add projects/your-project-slug/
git commit -m "Add project: Your Project Name"
git push -u origin HEAD
```

Do not edit `dev/generated/projects.json` or the project list in `README.md` — those are generated after merge.

✅ **Checkpoint:** Your branch is on GitHub.

---

### Step 9: Open a Pull Request

```bash
gh pr create --repo onlyfossorg/awesome-foss --title "Add project: Your Project Name" --body "$(cat <<'EOF'
- [x] Project repo has `README.md`, `CONTRIBUTING.md`, and `LICENSE.md` (or `LICENSE`)
- [x] `project.json` added
- [x] `README.md` included in `projects/<slug>/`
- [x] Folder name matches slug
EOF
)"
```

After pushing, you can also open the PR from GitHub: visit [onlyfossorg/awesome-foss](https://github.com/onlyfossorg/awesome-foss) and use **Compare & pull request**.

### Title Format:

```
Add project: Your Project Name
```

### Description:

Briefly describe your project and check the boxes:

```
- [x] Project repo has `README.md`, `CONTRIBUTING.md`, and `LICENSE.md` (or `LICENSE`)
- [x] `project.json` added
- [x] `README.md` included in `projects/<slug>/`
- [x] Folder name matches slug
```

✅ **Checkpoint:** Your PR is submitted! The automated CI will now validate your changes.

---

## Field Reference

Complete details for `project.json`:

| Field                      | Type    | Required | Description                                                      | Examples                                          |
| -------------------------- | ------- | -------- | ---------------------------------------------------------------- | ------------------------------------------------- |
| `slug`                     | string  | ✅       | Unique identifier. Lowercase kebab-case. Must match folder name. | `"lan-share-app"`, `"ai-chatbot"`                 |
| `name`                     | string  | ✅       | Display name (1-100 characters).                                 | `"LAN Share App"`, `"AI Chatbot"`                 |
| `tagline`                  | string  | ✅       | One-line description (1-150 characters).                         | `"Share files directly over your local network"`  |
| `description`              | string  | ✅       | Detailed explanation (10-500 characters).                        | `"A peer-to-peer file sharing application..."`    |
| `status`                   | string  | ✅       | Project state.                                                   | `"active"`, `"dormant"`, `"idea"`                 |
| `difficulty`               | string  | ✅       | Contributor difficulty level.                                    | `"beginner"`, `"intermediate"`, `"advanced"`      |
| `tech_stack`               | array   | ✅       | Technologies used. At least one required.                        | `["React", "Node.js", "Socket.io"]`               |
| `github_repo`              | string  | ✅       | Full GitHub URL. Must start with `https://github.com/`           | `"https://github.com/onlyfossorg/project"`          |
| `maintainers`              | array   | ✅       | At least one with `name` and `contact`.                          | `[{"name": "John", "contact": "john@email.com"}]` |
| `looking_for_contributors` | boolean | ✅       | Whether you want contributors.                                   | `true` or `false`                                 |
| `domain`                   | array   | ✅       | Project categories.                                              | `["Web"]`, `["AI/ML", "GenAI"]`                   |

**Valid `domain` values:**

- `"Web"` — Web applications, sites, or tools
- `"AI/ML"` — Artificial Intelligence and Machine Learning
- `"GenAI"` — Generative AI (ChatGPT-like, image generation, etc.)
- `"Blockchain"` — Cryptocurrency, smart contracts, decentralized apps
- `"IoT/Embedded"` — Internet of Things, hardware, embedded systems

## Need Help?

- 💬 [GitHub Discussions](https://github.com/onlyfossorg/awesome-foss/discussions) — Ask questions
- 🐛 [GitHub Issues](https://github.com/onlyfossorg/awesome-foss/issues) — Report problems
- 📚 [CONTRIBUTING.md](CONTRIBUTING.md) — Learn about the repo structure

---

**Every great project starts with a single commit. Welcome to ONLY FOSS ORG! 🚀**
