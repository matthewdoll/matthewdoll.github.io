# Personal site — deploy notes

Plain HTML/CSS/JS, no build step. Four pages: Home, Projects, CV, Contact.
Domain: **matthewdoll.co.uk** — a `CNAME` file with that domain is already in this repo.

## 1. Before you push

- **Contact form**: open `contact.html`, sign up free at formspree.io with mattdollr@gmail.com, create a form, and replace `YOUR_FORM_ID` in the form's `action` with your real endpoint. Until you do this, the form won't send anywhere.
- **CV**: `cv.html` is your redacted CV — phone number and address removed, and it's excluded from search indexing (`noindex`). Check it over before publishing.

## 2. Create the GitHub repo and push

Use `matthewdoll.github.io` as the repo name — serves at the root even with the custom domain, and gives a clean fallback URL if the domain's ever off.

```bash
cd personal-site
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/matthewdoll/matthewdoll.github.io.git
git push -u origin main
```

## 3. Turn on GitHub Pages

Repo → **Settings → Pages** → under "Build and deployment", set **Source: Deploy from a branch**, **Branch: main / (root)**. Save.

## 4. Point matthewdoll.co.uk at it via Cloudflare

**a. Get the domain onto Cloudflare's nameservers** (skip if already done):
1. Cloudflare dashboard → **Add a site** → `matthewdoll.co.uk` → Free plan.
2. Cloudflare gives you two nameservers. Go to wherever you bought the domain (registrar account) and replace its nameservers with those two.
3. This can take anywhere from a few minutes to ~24h to propagate (`.co.uk` via Nominet is usually fast, but not instant). Cloudflare emails you once it's active.

**b. Add the DNS records** (Cloudflare → DNS → Records, once the site is active):

| Type | Name | Content | Proxy status |
|---|---|---|---|
| A | `matthewdoll.co.uk` (@) | `185.199.108.153` | DNS only |
| A | `matthewdoll.co.uk` (@) | `185.199.109.153` | DNS only |
| A | `matthewdoll.co.uk` (@) | `185.199.110.153` | DNS only |
| A | `matthewdoll.co.uk` (@) | `185.199.111.153` | DNS only |
| CNAME | `www` | `matthewdoll.github.io` | DNS only |

Keep these **DNS only** (grey cloud) at first — Cloudflare's proxy can break GitHub's certificate check on initial setup.

**c. Set the custom domain in GitHub:**
1. Repo → **Settings → Pages → Custom domain** → enter `matthewdoll.co.uk` → Save. (The `CNAME` file already in the repo means this may already show as verified.)
2. Wait for the DNS check to go green, then tick **Enforce HTTPS** once it's available (can take a few hours).
3. Once HTTPS is enforced, you can switch the five DNS records above back to **Proxied** (orange cloud) if you want Cloudflare's CDN/caching/bot-protection in front of the site — optional, not required.

## 5. Adding projects

Each new project is a page under `projects/`, linked from a card in `projects.html`. Template block for the card is commented at the bottom of `projects.html`.
