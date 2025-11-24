# Wadelabs — Mini Landing

Standalone static site intended to be its own repository and published to a custom domain (https://wadelabs.io).

Quick steps to create a repository and publish to GitHub Pages with a custom domain

Checklist
- [x] Ensure `CNAME` file contains `wadelabs.io` (already set)
- [x] Confirm `.github/workflows/deploy.yml` exists (build + deploy to `gh-pages`)
- [x] Update `package.json` `homepage` to your GitHub Pages URL

1) Initialize a new git repo and push to GitHub (WADELABS/wadelabs-mini)

```bash
cd mini-landing-site
git init
git add .
git commit -m "Initial mini landing"
# create the repo on GitHub (https://github.com/WADELABS/wadelabs-mini) or create via web UI
git branch -M main
git remote add origin git@github.com:WADELABS/wadelabs-mini.git
git push -u origin main
```

2) DNS configuration for `wadelabs.io`

- If you control `wadelabs.io`'s DNS, create the following records (for apex domain):
  - A 185.199.108.153
  - A 185.199.109.153
  - A 185.199.110.153
  - A 185.199.111.153

- If you're using Cloudflare, ensure the records are **not** proxied (disable the orange cloud) so GitHub can validate and serve the domain.

- GitHub Pages will provision TLS once the domain is validated. This can take a few minutes to a couple hours.

3) Confirm deployment

- The GitHub Actions workflow will run on push to `main` and build + publish `dist` to the `gh-pages` branch.
- The action will preserve the `CNAME` file so GitHub Pages config will be associated with `wadelabs.io`.

4) Local testing

```bash
npm install
npm run dev
# open http://localhost:5173
```

Notes
- The `homepage` field in `package.json` is set to `https://WADELABS.github.io/wadelabs-mini`. If you plan to use a different hosting approach, update accordingly.
- If you prefer manual deploy, run `npm run build` and push the `dist` contents to GitHub Pages branch or another host.
- If you need help adding the DNS records at your registrar, tell me the provider and I can give step-by-step instructions.
