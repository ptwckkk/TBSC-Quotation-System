[README.md](https://github.com/user-attachments/files/29623895/README.md)
# TBSC — FRP Boat Quotation System

A self-contained, browser-based quotation maker for The Boat Shop Corporation. It calculates FRP boat quotations from hull dimensions, laminate schedule, structural components, paint, accessories, engine, labor, construction timeline, overhead, contingency, and profit margin — all in one HTML file, no server or build step required.

## Run it locally

No installation needed. Just open `index.html` in any modern browser (Chrome, Edge, Firefox, Safari).

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPO.git
cd YOUR-REPO
open index.html      # macOS
# or: start index.html   (Windows)
# or: xdg-open index.html  (Linux)
```

## Deploy on Cloudflare Pages (free hosting)

Cloudflare Pages hosts this the same way GitHub Pages does — it's a static file, so there's nothing to build or configure. Two ways to deploy:

### Option A — Connect your GitHub repo (dashboard, no CLI)

1. Push this project to GitHub first (see the GitHub Pages section above, steps 1–2).
2. Go to the [Cloudflare dashboard](https://dash.cloudflare.com/) → **Workers & Pages → Create → Pages → Connect to Git**.
3. Select your repository.
4. Build settings:
   - **Framework preset:** None
   - **Build command:** *(leave empty)*
   - **Build output directory:** `/` (project root, since `index.html` lives at the top level)
5. Click **Save and Deploy**.
6. Cloudflare publishes the site at:
   ```
   https://YOUR-PROJECT-NAME.pages.dev
   ```
   Every future `git push` auto-redeploys it.

### Option B — Direct deploy from your computer (no GitHub needed)

Requires [Node.js](https://nodejs.org/) for the one-time `npx wrangler` command (Cloudflare's CLI). No account setup beyond a free Cloudflare account.

```bash
cd YOUR-REPO-FOLDER
npx wrangler pages deploy . --project-name=tbsc-quotation
```

The first run will prompt you to log in to Cloudflare in your browser. After that it uploads the folder as-is (just `index.html`, `README.md`, `.gitignore`) and gives you a live `https://tbsc-quotation.pages.dev` URL immediately. Re-run the same command any time you update `index.html` to redeploy.

### Custom domain (either option)

In the Cloudflare Pages project → **Custom domains**, you can attach a domain you manage in Cloudflare (e.g. `quotes.boatshopphilippines.com`) instead of the default `.pages.dev` URL.

## Deploy on GitHub Pages (free hosting)

1. **Create a new GitHub repository** (public or private — Pages works on both if you have GitHub Pro/Team for private, otherwise use a public repo).
2. **Push this project to it:**
   ```bash
   git init
   git add .
   git commit -m "Initial commit: TBSC FRP Boat Quotation System"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
   git push -u origin main
   ```
3. In your repository on GitHub, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Under **Branch**, select **main** and folder **/ (root)**, then **Save**.
6. GitHub will publish the site at:
   ```
   https://YOUR-USERNAME.github.io/YOUR-REPO/
   ```
   (First deploy can take a minute or two.)

No GitHub Actions workflow, build tools, or dependencies are required — it's a static HTML/CSS/JS file that GitHub Pages serves as-is.

## Data storage

All quotations, customers, boat templates, and the pricing database are saved in the browser's `localStorage` — scoped to whichever URL you're using (e.g. your GitHub Pages URL). This means:

- Data is **per-browser, per-device**. It does not sync across computers or between `localhost` and your GitHub Pages URL.
- Clearing browser data/cache will erase saved quotations.
- There is no backend database — this is intentional, per the original spec, for a simple, dependency-free tool.

If you later need multi-user syncing (e.g. your whole team editing the same quotations), that would require adding a real backend (e.g. Firebase, Supabase, or a small API) — the current app is single-user/local by design.

## Project structure

```
.
├── index.html   # the entire application (HTML + CSS + JS, single file)
└── README.md    # this file
```

## Customizing

- **Company details** (name, tagline, email): edit the `COMPANY` constant near the top of the `<script>` block in `index.html`.
- **Default pricing** (fiberglass/resin/gelcoat prices, labor rates, daily construction rate, engine packages, accessory & structural catalogs): editable directly in the app under **Pricing Database**, or by editing the `DEFAULT_PRICING` object in the source for factory defaults.
- **Boat templates**: manage from the **Boat Templates** page in the app, or edit `DEFAULT_TEMPLATES` in the source.

## License

Internal tool for The Boat Shop Corporation. Add a LICENSE file here if you intend to open-source or share this repository publicly.
