# CLAUDE.md

This file provides guidance for AI assistants working with this repository.

## Project Overview

**Generative AI for Beginners** is a 14-lesson (00-13) curriculum by Microsoft Cloud Advocates teaching how to build Generative AI applications. It is primarily an educational content repository — not a traditional software project. The content is Markdown lessons, Jupyter notebooks, and Python/JS example code.

**License:** MIT

## Repository Structure

```
00-course-setup/          # Environment setup instructions
01-introduction-to-genai/ # Lesson 1 (concept-focused)
02-exploring-and-comparing-different-llms/
03-using-generative-ai-responsibly/
04-prompt-engineering-fundamentals/
05-advanced-prompts/
06-text-generation-apps/
07-building-chat-applications/
08-building-search-applications/
09-building-image-applications/
10-building-low-code-ai-applications/
11-integrating-with-function-calling/
12-designing-ux-for-ai-applications/
13-continued-learning/
translations/             # cn/, ja-jp/, pt-br/ translations
docs/                     # Docsify site config
presentations/            # PDF/PPTX slide decks
images/                   # Repo-level images
.github/workflows/        # CI validation workflows
```

### Lesson Directory Pattern

Each lesson folder typically contains:
- `README.md` — Main lesson content (learning goals, concepts, exercises)
- Jupyter notebooks with dual SDK variants:
  - `notebook-azure-openai.ipynb` (Azure OpenAI)
  - `notebook-openai.ipynb` (OpenAI)
  - `solution.ipynb` (completed exercises)
- Python files: `app.py`, `assignment.py`, `solution.py`
- Optional `dotnet/` or JS subdirectories for alternative implementations
- `images/` folder for lesson-specific assets

## Languages and Tech Stack

- **Python 3** — Primary language for all code lessons
- **Jupyter Notebooks** — Interactive exercises
- **Markdown** — All lesson content
- **JavaScript/Node.js** — Some lesson examples (openai SDK ^4.10.0)
- **.NET/C#** — Optional alternative examples

### Key Python Dependencies (requirements.txt)

```
openai>=0.28.0, tiktoken, python-dotenv, pandas, numpy, matplotlib, ipywidgets, tqdm
```

### Key Node.js Dependencies (package.json)

```
openai ^4.10.0, docsify-to-pdf (dev)
```

## Development Setup

1. **Clone and set up environment variables:**
   ```bash
   cp .env.copy .env
   # Fill in AZURE_OPENAI_ENDPOINT, AZURE_OPENAI_DEPLOYMENT, AZURE_OPENAI_KEY,
   # and AZURE_OPENAI_EMBEDDINGS_DEPLOYMENT
   ```

2. **Install Python dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Install Node.js dependencies (if needed):**
   ```bash
   npm install
   ```

4. **GitHub Codespaces:** The repo includes `.devcontainer/devcontainer.json` for one-click Codespaces setup with Python 3 pre-configured.

## CI / Validation Workflows

PRs targeting `main` that modify `**.md` or `**.ipynb` files trigger the `validate-markdown.yml` workflow with four sequential checks:

1. **Check Broken Relative Paths** — All relative links must resolve correctly
2. **Check Paths Have Tracking** — Relative links must end with `?wt.mc_id=` or `&WT.mc_id=` tracking ID
3. **Check URLs Have Tracking** — URLs to github.com, microsoft.com, visualstudio.com, aka.ms, and azure.com must include tracking IDs
4. **Check URLs Don't Have Locale** — URLs must not contain country-specific locale segments like `/en-us/` or `/en/`

Uses: `john0isaac/action-check-markdown@v1.0.6`

There are no code linting or formatting CI checks.

## Critical Conventions for Content Changes

### Markdown and Links

- URLs must be wrapped in `[text](url)` format with no extra spaces
- Relative links must start with `./` or `../`
- All relative links must include a tracking ID: append `?wt.mc_id=<ID>` or `&WT.mc_id=<ID>`
- URLs to Microsoft-related domains (github.com, microsoft.com, visualstudio.com, aka.ms, azure.com) must include tracking IDs
- Never include country-specific locale in URLs (no `/en-us/`, `/en/`, etc.)
- Images must be stored in each lesson's `./images` folder with descriptive English names using characters, numbers, and dashes

### API Keys and Secrets

- Never hard-code API keys — use `.env` files loaded via `python-dotenv`
- The `.env.copy` template shows required variables (Azure OpenAI endpoint, deployment, key, embeddings deployment)
- `.env` is gitignored

### Translations

- No machine translations — only contribute if proficient in the language
- Translations must be submitted as complete units (no partial lesson translations)
- Translations live in `translations/<locale>/` directories

## Contribution Workflow

1. Fork the repository
2. Make changes on your fork
3. Submit a PR — Microsoft CLA bot will check for Contributor License Agreement
4. Automated validation workflows will check markdown/link conventions
5. Separate unrelated changes into different PRs
6. Combine typo/doc fixes into single PRs where appropriate

## Commands Reference

| Command | Purpose |
|---------|---------|
| `pip install -r requirements.txt` | Install Python dependencies |
| `npm install` | Install Node.js dependencies |
| `npm run convert` | Convert Docsify docs to PDF |
| `jupyter notebook` | Launch Jupyter for interactive lessons |

## File Types to Be Aware Of

- `.md` — Lesson content (validated by CI)
- `.ipynb` — Jupyter notebooks (validated by CI for links)
- `.py` — Python example code and exercises
- `.js` — Node.js example code
- `.env.copy` — Environment variable template (do not put secrets here)
- `.env` — Local secrets file (gitignored, never commit)
