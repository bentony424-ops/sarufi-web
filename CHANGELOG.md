# Sarufi Website — Update Changelog

## What was done

### Performance
- Extracted all 23 base64-embedded images out of `index.html` into real compressed `.jpg` files under `assets/images/`, with descriptive filenames (e.g. `project-maasai-national-polytechnic.jpg`).
- This dropped `index.html` from **2.3MB → ~56KB**. Images are now cacheable and load in parallel instead of blocking the page parse.

### SEO
- Added a real page title, meta description, canonical tag, Open Graph tags, and Twitter Card tags (all pointed at `https://bentony424-ops.github.io/sarufi-web/` for now).
- Added `robots.txt` and `sitemap.xml`.
- Generated a placeholder favicon (all standard sizes + `site.webmanifest`) and a placeholder social share image at `assets/social-preview.jpg`.

### Accessibility
- Every image-carrying element (carousels, values grid, project cards) now has `role="img"` + a descriptive `aria-label`, since these are CSS background images rather than `<img>` tags.
- Fixed two color-contrast failures found on inspection: the project "kWp" label text and the contact-band labels were both below WCAG AA; both now pass.

### Functionality / UX
- Built a working mobile hamburger menu — nav links were previously just disappearing below 980px with no way to access them.
- Added a real call-to-action: "Get a Free Quote" button in the top contact strip, and "Talk to Our Team" in the closing section.
- Fixed the address link, which pointed at the generic Google Maps homepage instead of your actual office location.

### Other
- Created a branded custom `404.html` page (GitHub Pages will use this automatically).

### Contact form
- Built a real contact form (name, email, phone, service dropdown, message) wired to Web3Forms with your access key.
- Client-side validation with inline error messages (required name/message, valid email format).
- Honeypot field for spam protection (invisible to real users, catches basic bots).
- Async submission via `fetch` — no page reload, shows a success/failure message inline.
- All three CTA buttons ("Get a Quote" / "Get a Free Quote" / "Talk to Our Team") now link straight to the form instead of just the quick-contact info band.
- **Note:** I couldn't do a live end-to-end test from my side (this environment can't reach external APIs), but the request matches Web3Forms' documented format exactly. Test it yourself by opening `index.html` locally and submitting the form before you deploy — you should get an email within a minute or two.

### Analytics
- Wired in your Cloudflare Web Analytics beacon snippet (token provided) on both `index.html` and `404.html`, so page views and 404 hits are both tracked.

### Legal pages
- Drafted `privacy-policy.html` and `terms-and-conditions.html`, matching the site's design.
- Grounded the privacy policy in Kenya's **Data Protection Act, 2019** (data subject rights, ODPC complaint route) rather than a generic GDPR template, since Sarufi is Kenya-registered.
- Explicitly states the site collects no cookies (true today — Cloudflare Web Analytics and Web3Forms don't use them) and names the actual third parties involved (Web3Forms, Cloudflare, GitHub).
- Added a small footer to `index.html` linking to both pages, with an auto-updating copyright year.
- **Important — read before publishing:** these are drafts, not legal advice. Two things need your sign-off specifically:
  1. Both pages have a `[add date when you publish this]` placeholder for the "last updated" date — fill this in when you go live.
  2. Under Kenya's DPA, businesses with **annual turnover above KES 5 million or more than 10 employees** must **register as a data controller with the ODPC** — this is separate from having a privacy policy on your site. I can't tell from here whether that threshold applies to Sarufi; worth checking with whoever handles your compliance/legal matters before launch.

### Brand assets
- Swapped in your real logo (`assets/sarufi-logo.png`) — no longer a broken image reference.
- Regenerated the favicon (all sizes + `.ico`) and the social preview image from your actual logo, replacing the placeholder navy/gold "S" graphics.

### Floating WhatsApp button
- Added a fixed WhatsApp button, bottom-right, on every screen size, linking to `https://wa.me/254717501501` (same number as your phone pill) and opening in a new tab.

### Office map
- Added an embedded Google Maps section (no API key needed) showing your office location, styled to match the site — rounded card, shadow, heading, and a "Get directions" link that opens full Google Maps in a new tab.
- Sits between the quick-contact band and the closing tagline section.

### Impact counter
- Added a two-part animated "Our Impact" section between Projects and the contact form, on a dark navy band for contrast.
- **Plastic waste side**: counts up to 430M tons/year (reusing the same verified figure already in your "scale of the problem" cards — not a new invented statistic), with a drifting, ember-like particle animation in warning orange, evoking pollution.
- **Solar side**: counts up to **242.6 kWp** — calculated by summing every project in your Projects section (104 + 49 + 20 + 19.6 + 30 + 20). If you add or update a project later, this number needs a manual update to match (it isn't auto-calculated from the DOM, just pre-computed once). Animated with a rotating sun-ray burst in gold, distinct in both motion and feel from the waste side.
- Both numbers count up with an easing animation the first time they scroll into view (not on every scroll).

### Merged in from the parallel build
- **Accessibility**: added a real skip-to-content link, wrapped the page content in a proper `<main>` landmark, and added visible focus outlines on every interactive element (links, buttons, form fields).
- **Project lightbox**: clicking (or Enter/Space on keyboard) any project card now opens a full-size modal with the *actual original branded project banner* — I pulled these 6 real banner images directly out of the other build's file rather than reusing my cropped thumbnails, since they were genuinely better assets. Closes on the × button, clicking outside, or Escape; focus returns to the card afterward.
- **Values grid reordered** to: Sustainability, Team Work, Technology, Integrity, Environmental Protection.

### Company profile corrections (from the PDF you sent)
- Removed the paragraph referencing the board of governance, shareholders, and sister companies (Mecen IPC Co. Ltd / Kawi Energy Group) from the About Us section, per your explicit instruction.
- Cross-checked the rest of About/Vision/Mission/Energy/PET copy against the actual PDF — it already matched closely, no other content changes were needed there.
- **Flagging, not changing:** the PDF lists a different phone number (+254 721 158974) and a different address (Kofisi Karen – Karen Rd) than what's currently live on the site (+254 717 501501, Nyati Sacco Plaza). I did not change these, since you'd previously and explicitly told me to keep Nyati Sacco Plaza. Worth a final check on your end for which contact details are current.

## Still needs your input

1. **Keep the impact counter in sync.** If you add, remove, or update a project's capacity in the Projects section later, remember to also update the `data-target="242.6"` value on the solar counter (in the `.impact-energy` card) to match the new total — it's a static number, not auto-calculated.
2. **Domain.** Everything currently points at `https://bentony424-ops.github.io/sarufi-web/`. If you buy `sarufigroup.com` later, tell me and I'll swap every reference (canonical, OG tags, sitemap, robots.txt) in one pass, plus add a `CNAME` file.
3. **ODPC registration.** You're checking this with your manager — let me know what you find out in case it needs a mention anywhere.
4. **"Last updated" dates** on the two legal pages — add the real date when you actually publish.

## Not possible yet
- Real page-speed scores (Lighthouse-style) — needs the site actually deployed and live.
- Verifying the site in Google Search Console — same reason, needs a live deployment first.
