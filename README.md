# Notebook Atlas — Public Notebook Library

A polished, searchable, public Jupyter notebook library. **No localhost required after deployment.** Hosted free with GitHub Pages.

## Features

- Search filenames, markdown and code across every `.ipynb` file.
- Categories from notebook subfolder names.
- Source preview for code and markdown cells (never executes code).
- Individual `.ipynb` downloads.
- Download All ZIP, assembled in the visitor's browser.
- Responsive, dark premium UI.
- Auto-deployment on GitHub pushes.

## Add your 20 notebooks

1. Open `public/notebooks/` and **delete** `python_basics.ipynb` if you don't want the demo notebook.
2. Copy your `.ipynb` files into `public/notebooks/`.
3. Optional: create subfolders such as `public/notebooks/Unit 1/`, `public/notebooks/NumPy/`, `public/notebooks/Pandas/`. Each subfolder name becomes a category. Files directly in `notebooks/` appear in **General**.
4. Do not manually edit `public/catalog.json`: the build script creates it from your notebooks.
5. Commit and push your changes. GitHub Actions updates the public website automatically.

**Important:** GitHub Pages is public. Never upload notebooks containing API keys, passwords, private datasets, or personal information. Large notebook outputs/images can make the site slow; clear unnecessary outputs before committing.

## Deploy free on GitHub Pages (recommended)

### Step 1 — Create repository

1. Sign in at https://github.com and create a **public** repository named `notebook-library` (or another name).
2. Unzip this package and upload its contents to the repository root. Upload the `.github/workflows/deploy.yml` file too. For an easy upload, use GitHub Desktop or Git commands.

### Step 2 — Upload with Git (Windows PowerShell)

Install Git if needed, then run in the extracted project directory:

```powershell
git init
git add .
git commit -m "Launch Notebook Atlas"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/notebook-library.git
git push -u origin main
```

Replace `YOUR_USERNAME` and the repository name. If the repository already has a README or commits, clone it first and copy the project files into that clone instead.

### Step 3 — Enable Pages

1. On GitHub, open the repository → **Settings** → **Pages**.
2. Under **Build and deployment**, choose **GitHub Actions** as the source.
3. Open **Actions** → **Deploy Notebook Atlas** to check the build/deployment. If needed, rerun the workflow.
4. After deployment, open:

   `https://YOUR_USERNAME.github.io/notebook-library/`

Replace the username and repository name. The website is accessible anywhere with internet. It is not tied to your laptop or localhost.

### Step 4 — Add or update notebooks later

Upload more `.ipynb` files into `public/notebooks/` using GitHub's **Add file → Upload files**, then **Commit changes**. Each commit to `main` automatically regenerates the searchable catalog and deploys the new version.

## Local preview (optional)

Requires Node.js 20.19+ or 22.12+.

```bash
npm install
npm run dev
```

Open the address printed by Vite. This is only for testing; the deployed site uses the public GitHub Pages URL.

## Other hosting: Vercel

Import your GitHub repository at https://vercel.com/new. Framework preset: **Vite**. Build command: `npm run build`. Output directory: `dist`. Vercel gives you a public `*.vercel.app` URL. GitHub Pages is already fully configured, so Vercel is optional.

## How search works

At build time, `scripts/build-catalog.mjs` reads notebook cells and writes `public/catalog.json` containing filenames, titles, category names, and searchable code/markdown text. The browser searches that index instantly. The index contains up to 300,000 characters per notebook; this is enough for typical learning notebooks but not an unlimited full-text index. Preview fetches the original notebook JSON. Download All ZIP fetches all notebooks and zips them client-side.

## Notes and limitations

- **Public read-only site:** notebook uploads and edits happen through GitHub, not through the website.
- **No notebook execution:** previews show raw code and markdown; use Jupyter/Colab to run notebooks.
- **Internet required:** viewing and downloading the hosted site needs internet. Download ZIP before an offline lab session.
- **File name collisions:** Download All ZIP uses notebook filenames; if different folders contain files with the same name, JSZip may overwrite an entry. Keep filenames unique.
- **GitHub Pages quotas:** large files or very large collections may require a different storage/hosting solution.

## Project structure

```text
notebook-library/
├── .github/workflows/deploy.yml
├── public/
│   ├── catalog.json (auto-generated)
│   └── notebooks/
│       └── python_basics.ipynb (demo)
├── scripts/build-catalog.mjs
├── src/main.jsx
├── src/style.css
├── index.html
├── package.json
├── vite.config.js
└── README.md
```
