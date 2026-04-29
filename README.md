# Hyper3D Website

Static HTML/CSS site for **Hyper3D Limited** — precision manufacturing for ANZ (CNC machining, sheet metal, injection moulding, post-finishing).

Built to be hosted free on **GitHub Pages** with a custom domain (`hyper3d.co.nz`) and a free **Web3Forms** contact form. No build step, no JS framework — just HTML, CSS and one Google Font.

---

## File structure

```
/
├── index.html                       Home
├── about.html                       About / company
├── industries.html                  Industries served
├── materials.html                   Materials catalogue
├── faq.html                         Frequently asked questions
├── contact.html                     Contact + quote form
├── 404.html                         Page-not-found
├── capabilities/
│   ├── index.html                   Capabilities hub
│   ├── cnc-machining.html
│   ├── sheet-metal.html
│   ├── injection-moulding.html
│   └── post-finishing.html
├── css/styles.css                   All styling (one file)
├── images/                          (empty — currently using Unsplash hot-links)
├── CNAME                            GitHub Pages custom domain (hyper3d.co.nz)
├── robots.txt
├── sitemap.xml
└── README.md                        This file
```

---

## Local preview

Open `index.html` directly in a browser, or for a more accurate test:

```bash
cd /Users/bruno/Projects/Hyper3d
python3 -m http.server 8000
# then open http://localhost:8000
```

---

## Before going live — three things to do

### 1. Get a Web3Forms access key (5 minutes)

The contact form currently has a placeholder access key. Get a real one:

1. Go to https://web3forms.com/
2. Enter `carter@hyper3d.co.nz` as the destination email
3. Copy the access key they email you
4. Open `contact.html` and find this line:
   ```html
   <input type="hidden" name="access_key" value="YOUR_ACCESS_KEY_HERE" />
   ```
5. Replace `YOUR_ACCESS_KEY_HERE` with the key
6. Free tier covers 250 form submissions/month — plenty for a precision manufacturing site

### 2. Push to GitHub Pages

```bash
cd /Users/bruno/Projects/Hyper3d
git init
git add -A
git commit -m "Initial Hyper3D site"

# Create a new repo on github.com (e.g. "hyper3d-site")
git remote add origin https://github.com/<your-username>/hyper3d-site.git
git branch -M main
git push -u origin main
```

Then in the GitHub repo:
- Go to **Settings → Pages**
- Source: **Deploy from a branch**
- Branch: **main**, folder: **/ (root)**
- Save

GitHub will deploy in ~1–2 minutes. The site will be live at `https://<your-username>.github.io/hyper3d-site/` first, then on `hyper3d.co.nz` once DNS is set up.

### 3. Point hyper3d.co.nz at GitHub Pages

The `CNAME` file already tells GitHub Pages to use `hyper3d.co.nz`. You also need to update DNS at the registrar where Carter bought the domain.

**Add these DNS records:**

For the apex domain (`hyper3d.co.nz`), four `A` records pointing to GitHub:

| Type | Name | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

Optionally, for `www.hyper3d.co.nz`:

| Type | Name | Value |
|------|------|-------|
| CNAME | www | `<your-username>.github.io` |

DNS changes can take up to 24h to propagate but usually take 10–60 minutes. Once live, GitHub will automatically issue a free SSL certificate. In the repo's **Settings → Pages**, tick **Enforce HTTPS** once available.

---

## Photography

Images are currently hot-linked from Unsplash for placeholder use. To replace with Carter's own photography:

1. Drop real photos into `/images/` (recommended sizes below)
2. In each HTML file, replace the `https://images.unsplash.com/...` URLs with `images/your-photo.jpg`

**Recommended sizes:**
- Hero photo: 2000 × 1200 px (JPEG, 80% quality, < 400 KB)
- Card images: 900 × 600 px (JPEG, 80% quality, < 150 KB each)
- About / two-column images: 1200 × 900 px

Compress with [squoosh.app](https://squoosh.app/) or `imagemagick` before uploading.

---

## Editing content

- Each page has the **header** and **footer** repeated inline (static site — no includes). If you change the navigation or footer, update it on every page. Search-and-replace works for repetitive edits.
- All styling lives in `css/styles.css`. CSS variables at the top let you change colours globally (`--navy`, `--cyan`, etc.).
- Phone number, email and tagline are repeated in the footer of every page — check `contact.html` and the footer in `index.html` for the canonical content.

---

## Brand

| Element | Value |
|---------|-------|
| Primary navy | `#0A2540` |
| Accent cyan | `#00B5E2` |
| Body text | `#1F2A37` |
| Muted | `#5B6B7B` |
| Font | Inter (Google Fonts) |
| Logo | Inline SVG (hexagon outline + HYPER3D wordmark) |

---

## Contact details on the site

- Email: `carter@hyper3d.co.nz`
- Phone: `+64 21 764 445`
- Region: New Zealand (serving NZ + AU)

If any of these change, search-and-replace across all HTML files.

---

## Costs

| Item | Cost |
|------|------|
| GitHub Pages hosting | Free |
| Web3Forms (250 submissions/mo) | Free |
| SSL certificate | Free (auto via GitHub) |
| Domain (`hyper3d.co.nz`) | Already owned by Carter |
| **Monthly total** | **$0** |

If form volume exceeds 250/month, Web3Forms paid plans start around USD $9/mo for 1,000 submissions.

---

## What's next (optional improvements)

- Real photography (swap Unsplash placeholders for Carter's own product photos)
- Case studies / portfolio section if Carter has named projects he can publish
- Add Google Analytics 4 or Plausible for visitor tracking
- Add a blog directory for SEO content (would benefit from a static site generator like Eleventy or Astro at that point)
- Add structured data (JSON-LD `Organization` schema) for richer Google search results
