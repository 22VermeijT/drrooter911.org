# Doctor Rooter 911 — Site handoff & next steps

Use this checklist after client approval and when assets are submitted. The site is ready to deploy as-is; the items below are optional or blocked on client input.

---

## Before you show the client

- [ ] **Quick pass in a browser** — Click through every nav link and the contact form; confirm mobile menu opens/closes; try “Skip to main content” (Tab from top of page).
- [ ] **Phone numbers** — Confirm (608) 244-9456, (414) 514-5970, (608) 741-0399, (608) 856-0100 are correct.
- [ ] **Copy** — If you use Southern Wisconsin / county messaging, ensure titles and meta on all pages match (no stray “Madison” in titles if you’ve switched to counties).
- [ ] **Images** — All service photos (plumbing repair, drain, sewer, TV inspection, water mitigation, porta potty) load from the project root.

---

## SEO & visibility (what’s done vs what to do next)

**Already on the site:** Unique titles and meta descriptions, canonicals, Open Graph, geo meta (US-WI), sitemap + robots.txt, Plumber + WebSite + BreadcrumbList schema, FAQPage on services, `serviceType` in schema, internal links to service-areas and services, one H1 per page.

**Biggest impact for Google rankings (off-site):**
- **Claim and complete Google Business Profile** — Correct NAP, hours, categories (e.g. Plumber, Emergency plumbing service), photos, and (over time) reviews. This drives a lot of local visibility.
- **Consistent NAP everywhere** — Same name, address, phone on the site, GBP, Yelp, BBB, HomeAdvisor, etc.
- **Links** — Local directories, chamber of commerce, trade sites, local news or “best plumber” lists.

**Optional later (on-site):** Add an **og:image** (e.g. 1200×630) for better shares; add more **location/service pages** (e.g. “Emergency plumber Milwaukee”) if you want to target more keywords; add **AggregateRating** schema when you have a stable review source (e.g. Google reviews count).

---

## When client approves the site

- [ ] **Deploy to Vercel**  
  - Connect repo (or drag project folder to [vercel.com](https://vercel.com)).  
  - Set production domain to `www.drrooter911.org` (or client’s final domain) in Vercel project settings.  
  - Custom 404: Vercel will serve `404.html` from the project root automatically.

- [ ] **Confirm domain**  
  - If the final URL is not `https://www.drrooter911.org`, do a project-wide find/replace for that domain in:  
    - All HTML files: `canonical`, `og:url`, and JSON-LD `url` / `item` fields.  
    - `sitemap.xml` (`<loc>` URLs).  
    - `robots.txt` (`Sitemap:` URL).

---

## When client sends logo / brand assets

- [ ] **Favicon**  
  - Replace the placeholder favicon (orange wrench SVG in `<head>`) with client’s favicon.  
  - Add:  
    - `favicon.ico` in project root (or linked in `<head>`).  
    - Optional: `apple-touch-icon` link for home-screen icons.  
  - Remove or update the existing `<link rel="icon" type="image/svg+xml" href="data:image/svg+xml,...">` in:  
    - `index.html`, `about.html`, `services.html`, `service-areas.html`, `contact.html`, `our-work.html`, `404.html`.

- [ ] **Logo in nav/footer** (optional)  
  - If they provide a logo image, replace the SVG wrench + “Doctor Rooter 911” text in the nav and footer with an `<img>` (include `alt="Doctor Rooter 911"`).

---

## When client approves contact form delivery

- [ ] **Formspree**  
  - Create a Formspree form and get the form endpoint (e.g. `https://formspree.io/f/xxxxx`).  
  - In `contact.html`:  
    - Set the form `action` to the Formspree URL and `method="POST"`.  
    - Remove the line in the submit handler that says `e.preventDefault(); // Remove this line when Formspree action is set` (so the form actually submits).  
  - Keep the honeypot field (`website_url`); Formspree will ignore it. Optionally add a Formspree hidden field (e.g. `_subject`) if you want a custom email subject.

---

## Optional later improvements (no client assets required)

- **Google Business Profile**  
  - Claim/verify listing; keep NAP, hours, and categories in sync with the site. Big impact on local SEO.

- **More SEO pages**  
  - Add city/service pages (e.g. “Plumber Madison WI”, “Drain Cleaning Milwaukee”) with unique copy and the same nav/footer. Add URLs to `sitemap.xml` and link from `service-areas.html` or the homepage.

- **Our Work in nav**  
  - If client wants “Our Work” visible: uncomment the “Our Work” links in nav and footer on all pages, and add `our-work.html` to `sitemap.xml`.

- **Mobile menu accessibility**  
  - Add `aria-expanded` and `aria-controls` on the mobile menu button and `id` on the menu panel for screen readers.

---

## What’s already done

- Static HTML + Tailwind CDN; no build step.  
- All main pages: canonicals, meta descriptions, Open Graph, Plumber + BreadcrumbList JSON-LD.  
- Sitemap and `robots.txt`; internal keyword links; FAQ schema on services.  
- Placeholder favicon (orange wrench); replace when logo is provided.  
- Contact form: honeypot for spam; submit handler shows success (form does not send anywhere until Formspree is set).  
- Custom `404.html` for broken links and Vercel.  
- Target domain used across the site: `https://www.drrooter911.org`.
