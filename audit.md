# Website Audit — Manav Hemnani Portfolio
**Date:** March 9, 2026
**Pages reviewed:** index.html, about.html, contact.html, work.html, praan.html, percept.html, swift.html, solsky.html

---

## 🔴 Critical Bugs (Breaking)

### 1. Broken Nav Links — `index.html` (lines 721–723)
The three nav anchor tags are malformed — they're never closed and have no visible link text. This means **Work, About, and Contact are completely non-functional** in the navigation on the homepage.

```html
<!-- Current (broken) -->
<li><a href="/pages/work.html"
<li><a href="/pages/about.html"
<li><a href="/pages/contact.html"

<!-- Should be -->
<li><a href="/pages/work.html">Work</a></li>
<li><a href="/pages/about.html">About</a></li>
<li><a href="/pages/contact.html">Contact</a></li>
```

### 2. Broken HTML Structure — Featured Card in `index.html` (lines 803–816)
The featured Praan card has a misplaced `</div>` that closes `.project-visual` prematurely after the `<img>` tag, leaving `.project-visual-label` and `.project-coord` spans floating in the wrong position, followed by an orphaned `</div>`. The badge ("Shipped") and coordinate text will not overlay the image correctly.

### 3. Missing Pages Referenced in `work.html`
Two project cards link to pages that **do not exist** in the folder:
- Card 1 → `/pages/finance.html` (missing)
- Card 6 → `/pages/crypto.html` (missing)

Clicking these will result in 404 errors.

### 4. Missing CSS Class — `work.html`
Card 1 uses `class="vis-fourbridges"` for its visual, but **no styles are defined** for `.vis-fourbridges` anywhere. The card visual area will be invisible/empty.

---

## 🟠 Content Mismatches & Inconsistencies

### 5. Wrong Project Content on Work Page (`work.html`)
The work page has significant content/link mismatches:

| Card | Links To | Visual Used | Description Matches? |
|------|----------|-------------|----------------------|
| Card 1 | `/pages/finance.html` | `vis-fourbridges` (undefined) | Uses Praan air purification description — wrong |
| Card 2 | `solsky.html` (wrong path) | `vis-finance` | Sol & Sky content — wrong visual |
| Card 3 | `/pages/praan.html` | `vis-petcare` | Describes a pet care Shopify brand — wrong for Praan |

The project titles, descriptions, categories, and visuals do not match each other or the actual linked pages.

### 6. Duplicate Praan Listing on Homepage (`index.html`)
The homepage shows Praan Air Ecosystem as **both card #1 (featured) and card #3**. Card #3 links to `praan.html` but has copy about VR table tennis ("Training requires a partner. VR removes that constraint") — this is Swift VR content under the wrong project name.

### 7. CSS Variable Naming Bug — `index.html`
In `index.html`, `--accent-blue` is set to `#f0ede6` (off-white/cream). In all other pages it's `#4a9eff` (actual blue). This causes the `.cta-btn` hover fill to be near-white, making the white button text **invisible on hover** on the homepage CTA button.

---

## 🟡 Placeholder Content Not Filled In

### 8. `about.html` — Large Sections of Unfilled Copy
Multiple content blocks contain template placeholders that are visible to visitors:

- **Location:** `[ City, Country ]`
- **The Work block:** `[ 2–3 sentences in your voice... ]` — entire first paragraph is a prompt/instruction
- **Background block:** `[ The industrial design → UX transition in your own words... ]` — entire block is a prompt
- **Photography interest:** `[ camera / format ]` and `[ where you've shot ]`
- **Music interest:** `[ a set, artist, or club that matters to you ]`
- **Sport interest:** `[ how seriously, what level ]`
- **Reading:** `[ Current book ]` and `[ one sentence on why ]`
- **Thinking about:** `[ A design question you keep returning to right now ]`
- Photo placeholders: 3 image slots showing emoji placeholders (🖼) with "Portrait or working photo," "Travel / photography shot," "Court, studio, anywhere"

### 9. `contact.html` — Multiple Placeholder Values
- Resume link: `href="[ resume link ]"` — broken/unset
- Email description: `[ your@email.com ]` — placeholder visible to users
- Instagram description: `"and [ what you post ]"`
- Resume date: `"updated [ month year ]"`
- Footer email: `href="mailto:[ your@email ]"` — broken link

---

## 🔵 Navigation & Link Issues

### 10. Wrong Relative Paths in `work.html`
Several links use relative paths that will break when navigating from `/pages/work.html`:
- `href="solsky.html"` → should be `/pages/solsky.html`
- `href="contact.html"` (in CTA and footer) → should be `/pages/contact.html`

### 11. Footer Links Use `#` Placeholders in `work.html`
```html
<li><a href="#">LinkedIn ↗</a></li>
<li><a href="#">Instagram ↗</a></li>
```
These are dead links. The actual LinkedIn/Instagram URLs are already correctly set in other pages — they just need to be copied here.

### 12. `contact.html` Footer Has Placeholder Links
```html
<li><a href="#">LinkedIn ↗</a></li>
<li><a href="#">Instagram ↗</a></li>
<li><a href="mailto:[ your@email ]">Email ↗</a></li>
```
Same issue as above — real URLs are used in the `<main>` section but placeholders were left in the footer.

### 13. Email Address in ALL CAPS
Throughout the site, the email is written as `HEMNANIMANAV@GMAIL.COM`. While email addresses are case-insensitive, this looks visually unpolished and can break some older mail clients. Should be `hemnanimanav@gmail.com`.

---

## ⚪ SEO & Accessibility

### 14. No Meta Descriptions on Any Page
None of the pages include a `<meta name="description">` tag. This hurts search engine visibility and social share previews. Each page should have a unique, descriptive 150–160 character summary.

### 15. `work.html` — Project Cards Animate to `opacity: 0` Before Scroll
The IntersectionObserver script sets all `.card` elements to `opacity: 0` and `transform: translateY(16px)` before they're observed. If JavaScript fails or runs slowly, all project cards will be invisible. A `<noscript>` fallback or an initial CSS class approach would be more resilient.

### 16. `index.html` — No `<meta name="description">`
The title tag reads "Manav Hemnani — Product Designer" but there is no description meta tag, Open Graph tags, or Twitter card tags. This affects how the site appears when shared on LinkedIn, which is especially relevant for a design portfolio.

---

## Summary

| Severity | Count | Issues |
|----------|-------|--------|
| 🔴 Critical | 4 | Broken nav, broken HTML structure, missing pages, missing CSS class |
| 🟠 Mismatch | 3 | Wrong project content on work page, duplicate Praan, CSS variable naming |
| 🟡 Placeholder | 2 pages | About page unfilled, Contact placeholders |
| 🔵 Link issues | 4 | Wrong relative paths, dead `#` links, ALL CAPS email |
| ⚪ SEO/A11y | 3 | No meta descriptions, JS-only card visibility, no OG tags |

**Priority order to fix:**
1. Fix broken nav links in `index.html` (visitors can't navigate)
2. Fix work.html — missing pages, mismatched content, wrong paths
3. Fill in all placeholder content in `about.html` and `contact.html`
4. Fix the featured card HTML structure in `index.html`
5. Fix the `--accent-blue` variable inconsistency in `index.html`
6. Add meta descriptions to all pages
7. Fix footer links on `work.html` and `contact.html`
