# Building Your Data Science Portfolio

**Jupyter Book 2 + MyST + GitHub Pages**

A complete guide from zero to a published portfolio website.

---

## 01 — Overview

This guide walks you through setting up, customizing, and deploying a professional Data Science portfolio built with Jupyter Book 2.

By the end, you will have:

- A local portfolio you can preview in your browser
- Jupyter notebooks styled as project case studies
- A live website at `https://YOUR_USERNAME.github.io/ds-portfolio/`
- A simple workflow for adding new projects throughout the semester

---

## 02 — What Changed from the Old Instructions

If your original assignment mentions `_config.yml`, `_toc.yml`, `jupyter-book create`, or `ghp-import`, those are **Jupyter Book 1** commands. This portfolio uses **Jupyter Book 2**, which is the current version.

| Old (Jupyter Book 1)            | Current (Jupyter Book 2)           |
| ------------------------------- | ---------------------------------- |
| `pip install jupyter-book<2`    | `pip install jupyter-book`         |
| `jupyter-book create my-book`   | `jupyter book init`                |
| `_config.yml` + `_toc.yml`     | `myst.yml` (single config file)    |
| `jupyter-book build .`          | `jupyter book build --html`        |
| `ghp-import` for deployment     | GitHub Actions (automatic)         |
| Sphinx-based engine             | MyST Document Engine               |

**Key difference:** Jupyter Book 2 uses the MyST Document Engine (JavaScript-based) instead of Sphinx (Python-based). The `myst.yml` file replaces both `_config.yml` and `_toc.yml`.

---

## 03 — Tools You Need

Before starting, verify you have these installed:

### Python 3.10+

```bash
python --version
```

If not installed, download from https://python.org. On macOS/Linux, you may need `python3` instead of `python`.

### Git

```bash
git --version
```

If not installed:
- **Windows:** Download from https://git-scm.com
- **macOS:** Install via Xcode command line tools: `xcode-select --install`
- **Linux:** `sudo apt install git` (Ubuntu/Debian)

### Node.js 18+

Jupyter Book 2 uses the MyST engine, which requires Node.js.

```bash
node --version
```

If not installed, download from https://nodejs.org (use the LTS version).

### A Code Editor

VS Code is recommended: https://code.visualstudio.com

---

## 04 — Project Structure

```
ds-portfolio/
├── myst.yml              ← Main configuration file
├── index.md              ← Homepage
├── about.md              ← About page
├── skills.md             ← Skills & toolkit
├── README.md             ← GitHub repository README
├── requirements.txt      ← Python dependencies
├── .gitignore            ← Files Git should ignore
├── assets/
│   └── custom.css        ← Portfolio visual styling
├── projects/
│   ├── index.md          ← Project gallery
│   ├── lab02-*.ipynb     ← Lab notebooks
│   ├── lab03-*.ipynb
│   ├── lab04-*.ipynb
│   ├── lab05-*.ipynb
│   └── lab06-*.ipynb
└── .github/
    └── workflows/
        └── deploy.yml    ← Auto-deploy workflow
```

---

## 05 — Installing Jupyter Book

### Step 1: Create a virtual environment

**Windows (PowerShell):**

```powershell
cd ds-portfolio
python -m venv .venv
.venv\Scripts\Activate.ps1
```

> **If PowerShell blocks the script:** You may see an error about execution policies. Run this once:
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> ```
> Then try activating again.

**macOS / Linux:**

```bash
cd ds-portfolio
python3 -m venv .venv
source .venv/bin/activate
```

You should see `(.venv)` in your terminal prompt.

### Step 2: Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

This installs Jupyter Book 2, NumPy, Pandas, Matplotlib, and the other packages listed in `requirements.txt`.

### Step 3: Verify installation

```bash
jupyter book --version
```

You should see a version number starting with `2.x`.

### About PyTorch

PyTorch is **not** included in `requirements.txt` because the correct version depends on your system (CPU vs. GPU, operating system). Install it separately:

1. Go to https://pytorch.org/get-started/locally/
2. Select your system configuration
3. Run the provided install command

For CPU-only (simplest):
```bash
pip install torch torchvision
```

---

## 06 — Understanding the Files

### myst.yml

This is the single configuration file for your entire portfolio. It defines:

- **Project metadata** — title, description, author, keywords
- **Table of contents** — which pages appear and in what order
- **Site settings** — theme, custom CSS, navigation links

The TOC section is the most important part. Every page in your portfolio must be listed here.

### index.md

Your homepage. Uses MyST Markdown, which extends standard Markdown with directives like `::::{grid}` for layouts and `:::{card}` for project cards.

### assets/custom.css

Controls the visual appearance. Edit the CSS variables at the top to change colors, spacing, and typography across the entire site.

### .github/workflows/deploy.yml

The GitHub Actions workflow that automatically builds and publishes your site whenever you push to `main`.

---

## 07 — Customizing Your Portfolio

### What to replace

Search for these placeholders across all files and replace them:

- `YOUR_NAME` — Your full name
- `YOUR_PROGRAM` — Your degree program (e.g., "BS Computer Science")
- `YOUR_YEAR_LEVEL` — Your year (e.g., "3rd Year")
- `YOUR_UNIVERSITY` — Your university name
- `YOUR_GITHUB_USERNAME` — Your GitHub username
- `YOUR_EMAIL` — Your email address
- `YOUR_LINKEDIN` — Your LinkedIn URL slug
- `YOUR_DATE` — The date you completed each lab

### Changing the accent color

Open `assets/custom.css` and find:

```css
--portfolio-accent: #2563EB;
```

Replace `#2563EB` with any color you prefer. Also update `--portfolio-accent-soft` and `--portfolio-accent-hover` to lighter and darker shades of the same hue.

---

## 08 — Adding Notebooks

### Replacing placeholder content

Each lab notebook in `projects/` contains structured placeholders marked with `<!-- REPLACE: ... -->` comments. To fill in your actual work:

1. Open the notebook in JupyterLab or VS Code
2. Replace placeholder cells with your implementation
3. Add your observations and analysis
4. Run all cells to generate output
5. Save the notebook

### Adding a completely new notebook

1. **Create** the notebook file in `projects/`:
   ```
   projects/my-new-project.ipynb
   ```

2. **Add it to the TOC** in `myst.yml`:
   ```yaml
   toc:
     - file: index.md
     - title: Projects
       children:
         - file: projects/index.md
         - file: projects/lab02-understanding-deep-learning.ipynb
         # ... existing entries ...
         - file: projects/my-new-project.ipynb    # ← add here
     - file: about.md
     - file: skills.md
   ```

3. **Add a card** to `projects/index.md` (optional but recommended):
   ```markdown
   :::{card} My New Project Title
   :link: my-new-project
   Brief description of the project.

   **Tools** — Python · Pandas · scikit-learn
   :::
   ```

4. **Preview** with `jupyter book start` to check everything looks right.

---

## 09 — Previewing Locally

```bash
jupyter book start
```

This starts a local development server. Open the URL shown in your terminal (usually `http://localhost:3000`).

**Live preview:** Changes to `.md` files are reflected automatically. For `.ipynb` changes, you may need to refresh the page.

**To stop the server:** Press `Ctrl+C` in your terminal.

---

## 10 — Publishing to GitHub

### Step 1: Create a GitHub repository

1. Go to https://github.com and sign in (or create an account)
2. Click the **+** button → **New repository**
3. Name it `ds-portfolio`
4. Choose **Public** (required for free GitHub Pages)
5. Do **not** initialize with README, .gitignore, or license (you already have these)
6. Click **Create repository**

### Step 2: Push your code

From your project directory:

```bash
git init
git add .
git commit -m "Initial Data Science portfolio"
git branch -M main
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/ds-portfolio.git
git push -u origin main
```

Replace `YOUR_GITHUB_USERNAME` with your actual GitHub username.

---

## 11 — GitHub Pages Deployment

### Enable GitHub Pages

1. In your repository, go to **Settings**
2. Click **Pages** in the left sidebar
3. Under **Build and deployment → Source**, select **GitHub Actions**
4. That's it — the workflow file you pushed will handle the rest

### Check deployment status

1. Go to the **Actions** tab in your repository
2. You should see a workflow run triggered by your push
3. A green checkmark means success; a red X means failure
4. Click on a failed run to see error logs

### Your site URL

After successful deployment, your site is live at:

```
https://YOUR_GITHUB_USERNAME.github.io/ds-portfolio/
```

It may take 1–2 minutes after the first deployment.

---

## 12 — Updating Your Portfolio

Every time you modify your portfolio, follow this routine:

```bash
# 1. Check what changed
git status

# 2. Stage all changes
git add .

# 3. Commit with a descriptive message
git commit -m "Add Lab 3 notebook"

# 4. Push to GitHub
git push
```

GitHub Actions will automatically rebuild and redeploy your site. You do **not** need to run any build commands or use `ghp-import`.

---

## 13 — Troubleshooting

### "jupyter: command not found" or "jupyter book: not recognized"

Your virtual environment is not activated. Run:
- **Windows:** `.venv\Scripts\Activate.ps1`
- **macOS/Linux:** `source .venv/bin/activate`

### "node: command not found"

Node.js is not installed. Download it from https://nodejs.org.

### PowerShell execution policy error

Run once in PowerShell as Administrator:
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### YAML indentation error in myst.yml

YAML is whitespace-sensitive. Use **spaces, not tabs**. Every indentation level should be exactly 2 spaces. Use VS Code with a YAML extension for visual feedback.

### Notebook missing from navigation

Every notebook must be listed in the `toc` section of `myst.yml`. If a file exists in `projects/` but is not in the TOC, it won't appear in the site navigation.

### Broken links to projects

Make sure the `link` value in your `:::{card}` directives matches the filename (without extension) in `projects/`. For example, if the file is `lab02-understanding-deep-learning.ipynb`, the link should be `lab02-understanding-deep-learning`.

### Images not showing

- Check that image paths are relative to the file that references them
- Ensure the image file is committed to Git (check `.gitignore`)

### "git: command not found"

Install Git from https://git-scm.com.

### "remote origin already exists"

If you get this error when adding a remote:
```bash
git remote remove origin
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/ds-portfolio.git
```

### "rejected" Git push

If your push is rejected, it usually means the remote has changes you don't have locally:
```bash
git pull --rebase origin main
git push
```

### GitHub Pages shows 404

- Verify Pages is set to deploy from **GitHub Actions** (not a branch)
- Check the Actions tab for build errors
- Wait 1–2 minutes after a successful build
- Make sure your repository is named `ds-portfolio` (case matters in URLs)

### GitHub Action failed

Click on the failed run in the **Actions** tab and expand the failing step. Common issues:
- Missing `requirements.txt` packages
- Invalid `myst.yml` syntax
- Notebook references files that don't exist in the repo

### CSS not loading

Verify the path in `myst.yml` matches your actual file:
```yaml
site:
  options:
    style: assets/custom.css
```

### Plotly chart not rendering

Plotly charts require the Plotly JavaScript library. In Jupyter Book 2, Plotly output should render as static images by default. For interactive Plotly:
- Use `plotly.io.write_html()` to save interactive versions
- Or use Matplotlib for static charts if interactivity isn't needed

### Notebook output is too large

Large outputs (big DataFrames, many plots) can slow down builds. Use:
- `df.head()` instead of printing entire DataFrames
- Save large figures at reasonable resolution
- Clear unnecessary cell outputs before committing

### Accidentally committed secrets

If you committed API keys or passwords:
1. Remove them immediately from the file
2. Consider the secret compromised — rotate/regenerate it
3. Use a `.env` file (added to `.gitignore`) for secrets going forward

---

## 14 — Quick Command Reference

### Start your environment

**Windows PowerShell:**
```powershell
cd ds-portfolio
.venv\Scripts\Activate.ps1
```

**macOS / Linux:**
```bash
cd ds-portfolio
source .venv/bin/activate
```

### Preview your portfolio

```bash
jupyter book start
```

### Build static HTML

```bash
jupyter book build --html
```

Output goes to `_build/html/`.

### Update your live site

```bash
git add .
git commit -m "Update portfolio"
git push
```

### Add a new notebook to the TOC

In `myst.yml`, under `project.toc`, add:
```yaml
- file: projects/your-notebook.ipynb
```

### Check Git status

```bash
git status
git log --oneline -5
```
