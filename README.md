# Data Science Portfolio

A portfolio of deep learning experiments and data science projects —
built with [Jupyter Book 2](https://jupyterbook.org/) and published
on GitHub Pages.

Live website: https://gabramschool-commits.github.io/DS-DeepLearning/
---

## Technology

| Layer         | Tool                            |
| ------------- | ------------------------------- |
| Content       | Jupyter Notebooks, MyST Markdown |
| Build engine  | Jupyter Book 2 (MyST Engine)     |
| Theme         | book-theme + custom CSS          |
| Hosting       | GitHub Pages via GitHub Actions  |
| Analysis      | Python, NumPy, PyTorch           |
| Visualization | Matplotlib, Seaborn              |

---

## Project Structure

```
ds-portfolio/
├── myst.yml              ← Book configuration
├── index.md              ← Homepage
├── about.md              ← About page
├── assets/
│   └── custom.css        ← Portfolio styling
├── projects/
│   ├── index.md          ← Project gallery
│   ├── lab02-forward-propagation.ipynb
│   ├── lab03-forward-backward-propagation.ipynb
│   ├── lab04-regression-pytorch.ipynb
│   ├── lab05-pytorch-tensor-basics.ipynb
│   └── lab06-cnn-architecture.ipynb
├── requirements.txt
└── .github/
    └── workflows/
        └── deploy.yml    ← Auto-deploy to GitHub Pages
```

---

## Quick Start

```bash
git clone https://github.com/gabramschool-commits/DS-DeepLearning.git
cd DS-DeepLearning
pip install jupyter-book
jupyter book start
```

The site opens at `http://localhost:3000`.

---

## Adding a New Project

1. Place your `.ipynb` file in `projects/`.
2. Open `myst.yml` and add the file under `project.toc`.
3. Add a card to `projects/index.md` if desired.
4. Preview with `jupyter book start`.
5. Commit and push — GitHub Actions deploys automatically.

---

