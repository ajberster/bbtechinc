# Build the bbtechinc.com splash page

Build a single-page static site for **BBTech Inc.**, deployable to GitHub Pages with HTTPS on the apex domain `bbtechinc.com`.

## Read this first — the logo is unusual

The axe **is** the letter T. The wordmark is **ECH**, not TECH. Read together the lockup spells BBTECH.

Non-negotiable rules from the logo book:

- Never place a separate T before ECH
- Never letter "TECH" in type next to the mark
- Never stretch, distort, or change proportions or spacing
- Never add shadows, glows, gradients, or outlines
- Keep the axe fully visible — nothing overlaps it, nothing crops it

Because "axe + ECH" only resolves for someone who already knows the trick, **spell out `BBTECH INC.` in plain type in the nav**. That's the one place the full name appears as text, and it teaches the mark on first view.

## Before you write anything

Run `ls -R images/logos` and read the actual filenames. Do not guess. There are PNG exports in three variants — black on white, reversed white on black, and transparent — plus SVG masters and possibly an ICO.

Three approved assets exist. Map them like this:

| Asset | Where it goes |
|---|---|
| Standalone mark, transparent, black | Nav, at ~30px tall |
| Primary full lockup, transparent, black | Hero, large |
| Reversed lockup (white artwork) | The black statement band |
| Standalone mark, smallest black | Favicon |

There is no horizontal or vertical lockup variant. Do not invent one by repositioning parts of the primary lockup.

Prefer SVG where a master exists; otherwise use the largest PNG with explicit `width`/`height` so nothing shifts on load. Reference files on disk with `<img>` — do not inline base64 and do not redraw the logo in code.

## Stack

Plain HTML and CSS. No framework, no build step, no npm. One `index.html`, one `styles.css`. GitHub Pages serves it as-is.

Also create `CNAME` containing exactly `bbtechinc.com`, an empty `.nojekyll`, a permissive `robots.txt`, and wire the favicon in `<head>`.

## Design system

```css
--ink:        #0A0A0A;   /* body text */
--ink-soft:   #44403C;   /* paragraphs */
--ink-muted:  #78716C;   /* labels, footer */
--teal:       #0D9488;   /* primary accent */
--teal-light: #14B8A6;   /* hover states */
--teal-glow:  #2DD4BF;   /* accents on the black band only */
--rule:       #E7E5E4;   /* hairlines */
--paper:      #FFFFFF;
--black:      #0A0A0A;   /* statement band background */
```

Type: system sans — `-apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif`. Two weights only, 400 and 500. Never 600 or 700.

Small labels are uppercase, 11–12px, 2.5–4.5px letter-spacing. Body copy 16–17px at 1.65 line-height.

Teal appears only as: the 2px rule under the nav, the short rule under the tagline, tagline text, section numerals, and venture-card top borders. **Never as a background fill.** On a black-and-white page one accent color dies the moment you use it as a surface.

Hairlines at 0.5px. Square corners throughout.

## Page structure

**1. Nav** — standalone mark at ~30px on the left, then `BBTECH INC.` in type beside it at 13px/500 with 1.6px letter-spacing. Nothing on the right. 2px solid teal bottom border. Sticky.

**There are no links anywhere on this page** — no nav links, no email, no `mailto:`, no social, no external URLs. Not a single `<a>` tag. This is deliberate. Do not add a contact section, a form, or a "get in touch" line to fill the gap.

**2. Hero** — centered. Primary full lockup at ~260px tall. Below it a 48×3px teal rule, then in teal:

> POWERING WHAT'S NEXT

Then one paragraph, max-width ~560px:

> A holding company built on strength, precision, and innovation. We build, acquire, and hold — across software, real assets, and capital. One entity, many ventures, no expiration date.

Give the lockup clear space on all sides equal to at least the cap height of the E in the wordmark. At the specified size that's roughly 30px. Nothing intrudes.

**3. Three pillars** — three columns divided by 0.5px vertical rules. Teal numeral, heading, two lines.

- **01 Strength** — Durable positions held for decades, not quarters. We don't take on obligations that force our hand.
- **02 Precision** — Few bets, deeply understood before capital moves. Concentration beats diversification when you do the work.
- **03 Innovation** — Systems built in-house, then put to work. What we learn operating one venture compounds into the next.

**4. Statement band** — full-bleed black. Reversed lockup on the left at ~140px, copy on the right. Eyebrow in `--teal-glow`:

> THE THESIS

> Patient capital compounds. We back what we can build, buy what we can improve, and hold what we understand. There's no fund clock, no committee, and no pressure to exit a good position early. The best returns come from being able to wait — so we've structured everything around being able to.

**5. Ventures** — eyebrow label, then three cards. Each: 0.5px border, 2px solid teal top border, zero radius, heading, one line. Static — no hover effect, since nothing here is clickable and a card that reacts to the cursor implies it does something.

- **Software** — Products and platforms, built and operated.
- **Real assets** — Property and holdings with long horizons.
- **Capital** — Positions, partnerships, and patient equity.

One muted line under the grid: *Individual ventures operate at their own subdomains.*

**6. Footer** — 0.5px top rule. `BBTECH INC.` uppercase and letter-spaced on the left, `POWERING WHAT'S NEXT` in muted gray on the right. Below, centered and muted: `© 2026 BBTech Inc.` No email, no links.

## Copy rules

Nothing on this page names a specific business, product, client, or asset. Posture and approach only — the site is a stable front door for subdomains that will come and go.

Sentence case in prose. Uppercase only in the small letter-spaced labels.

## Responsive

Breakpoint at 768px. Below it: pillars stack to one column with horizontal rules; the statement band stacks and centers; venture cards go full width; the hero lockup drops to ~170px.

Below 480px, swap the hero from the full lockup to the **standalone mark** at ~120px and set `BBTECH INC.` beneath it in type at 20px/500. Per the logo book, the full lockup is only used when ECH and INC stay legible — at phone widths they don't.

## Quality bar

- Semantic HTML: one `<h1>`, `<nav>`, `<main>`, `<section>`, `<footer>`
- The `<h1>` is visually the hero lockup; give the `<img>` `alt="BBTech Inc."` so screen readers get the name, since the mark spells it graphically
- Decorative logo repeats use `alt=""`
- No interactive elements, so no focus states are needed — but do not disable focus outlines globally either
- No animation or transitions at all, so `prefers-reduced-motion` needs no special handling
- Full `<head>`: title, meta description, canonical, Open Graph and Twitter tags pointing at a logo PNG, `theme-color` `#0A0A0A`
- WCAG AA contrast — check teal on white specifically
- No external requests. No web fonts, no analytics, no CDNs. Must render offline from the filesystem.

## When done

Print the exact steps to point Cloudflare DNS at GitHub Pages for the apex domain — the four A records and the AAAA records — and note that "Enforce HTTPS" must be enabled in repo settings once DNS propagates. Assume Cloudflare is in DNS-only mode.
