# Deploying dhistack.ai to Cloudflare Pages

This is a static site (no build step). Cloudflare Pages hosts it free, with unlimited
bandwidth, free SSL, and a global CDN. Your domain is already on Cloudflare, so the
custom-domain step is one click.

There are two ways to deploy. **Option A (Connect to Git)** is recommended — every push
to GitHub then auto-deploys. **Option B (Direct Upload)** is the fastest if you just want
it live right now without GitHub.

---

## Option A — Connect to Git (recommended, auto-deploys)

### 1. Make sure the repo is pushed
In Terminal, from the project folder:
```
cd "/Users/ammus/Documents/Vaaro_Claude/DHISTACK.AI WEBSITE/DHISTACK.AI"
git add -A
git commit -m "Update site"
git push
```

### 2. Create the Pages project
1. Go to the Cloudflare dashboard → **Workers & Pages**.
2. Click **Create** → **Pages** tab → **Connect to Git**.
3. Authorize GitHub if asked, then select the **`dhistack.ai`** repository.

### 3. Build settings
Because this is plain HTML (no framework), use:
- **Framework preset:** `None`
- **Build command:** *(leave empty)*
- **Build output directory:** `/`  *(root — that's where index.html lives)*

Click **Save and Deploy**. In ~30 seconds you get a live URL like
`dhistack-ai.pages.dev`.

### 4. Add your custom domain
1. Open the new Pages project → **Custom domains** tab → **Set up a domain**.
2. Enter `dhistack.ai` → **Continue** → **Activate**. Cloudflare adds the DNS record
   automatically because the domain is on the same account.
3. Repeat for `www.dhistack.ai` if you want the www version too.

Done — you're live on **https://dhistack.ai** with HTTPS. From now on, every
`git push` redeploys automatically.

---

## Option B — Direct Upload (no GitHub needed)

1. Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** →
   **Upload assets**.
2. Name the project `dhistack`.
3. Drag in the site files — **`index.html`**, `motion-lab.html` (skip the `backups/`
   folder). Or drag the whole folder.
4. Click **Deploy**, then add the custom domain exactly as in Option A, step 4.

The downside: you must re-upload manually each time you change the site. Option A avoids
that.

---

## Notes
- **Output directory is the root** (`/`) because `index.html` sits at the top level.
- No environment variables, no build tools, nothing to configure.
- To preview locally before deploying, just open `index.html` in a browser, or run
  `python3 -m http.server` in the folder and visit `http://localhost:8000`.
