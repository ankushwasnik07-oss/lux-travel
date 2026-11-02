# 🚀 Deploying Infinity Travels on Vercel

### What caused the build error?
Vercel previously displayed:
> `No Flask entrypoint found. Set "tool.vercel.entrypoint" in pyproject.toml or define an entrypoint in one of: app.py, index.py...`

This happens when Vercel detects Python files or has the **Flask** preset selected in the Vercel dashboard, but no standard Flask entrypoint (`app.py`, `api/index.py`) was present at the root.

---

### What has been fixed:
1. **Added `app.py`**: A fully functional Flask WSGI application with REST endpoints (`/api/packages`, `/api/quote`, `/api/book`, `/api/health`) and static frontend serving.
2. **Added `api/index.py`**: Vercel Serverless Function entrypoint so API calls automatically map to Python.
3. **Added `pyproject.toml`**: Configured `[tool.vercel] entrypoint = "app.py"` as instructed by Vercel's build detector.
4. **Added `requirements.txt`**: Added `flask>=3.0.0`, `werkzeug>=3.0.0`, `requests>=2.31.0` so Vercel installs the necessary Python dependencies during build.
5. **Added `vercel.json`**: Configured `"framework": "vite"`, build command `npm run build`, and SPA output directory `dist` with rewrites.

---

### How to Deploy (Step-by-Step):

#### Method 1: Using Vercel Dashboard (Recommended)
1. Go to [vercel.com](https://vercel.com) and click **"Add New..." > "Project"**.
2. Import your GitHub / Git repository.
3. In the **Configure Project** screen:
   - **Framework Preset**: Select **Vite** (or leave default detected).
   - **Root Directory**: `./` (project root).
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
   - **Install Command**: `npm install`
4. Click **Deploy**. Your site will build and go live in seconds!

#### Method 2: Deploying via Vercel CLI
```bash
npm install -g vercel
vercel
```
Accept the defaults and deploy!
