# Contributing to LanView CLI

Thanks for your interest in contributing to **LanView CLI**! 🎉

LanView is an open-source, zero-config tool that bridges your frontend and backend into a single local gateway with a scannable terminal QR code for instant mobile testing.

---

## 🚀 Quick Setup

1. **Fork and clone** the repo:
   ```bash
   git clone https://github.com/<YOUR-USERNAME>/lanview-cli.git
   cd lanview-cli
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Link for local testing**:
   ```bash
   npm link
   ```
   Now running `lanview` in any terminal will use your local code.

4. When done testing, you can unlink with:
   ```bash
   npm unlink -g lanview
   ```

---

## 🛠️ How to Contribute

1. **Pick an issue or feature**:
   - Check open [GitHub Issues](https://github.com/PrashantDhuri08/lanview-cli/issues).
   - Feel free to report bugs, suggest features, or improve documentation.

2. **Create a branch**:
   ```bash
   git checkout -b feat/your-feature-name
   # or
   git checkout -b fix/your-bug-fix
   ```

3. **Make your changes**:
   - Keep changes clean, focused, and well-tested.
   - Test both proxy mode (`lanview`) and static mode (`lanview --static`).

4. **Commit & Push**:
   ```bash
   git commit -m "feat: description of changes"
   git push origin feat/your-feature-name
   ```

5. **Open a Pull Request**:
   - Submit your PR against the `main` branch.
   - Include a brief description of what you changed and why.

---

## 📬 Need Help?

- **Repository**: [github.com/PrashantDhuri08/lanview-cli](https://github.com/PrashantDhuri08/lanview-cli)
- **Maintainer**: Prashant Dhuri ([prashantdhuripd6@gmail.com](mailto:prashantdhuripd6@gmail.com))
