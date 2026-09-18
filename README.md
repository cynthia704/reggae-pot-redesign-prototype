# Reggae Pot Jamaican Grill — Redesign Prototype

**Built:** September 15, 2026 · **Status: Coded prototype, two pages (Home + Menu), not connected to WordPress**
**Files:** `index.html` (homepage), `menu/index.html` (menu page), and a shared `assets/` folder + `assets/site.css` (real photos, logo, and video pulled from the live site, plus the styles both pages share). Open either `index.html` directly in a browser — relative paths need `assets/` to sit alongside them, so keep the whole folder together if you move or share this.

> **Scope note.** This is one page (the homepage) built to prove out the fix and the direction, not a finished 8-page site. Built after Beth's Sep 14 "start the redesign" to-do (due Sep 18) — see `SESSION-NOTES.md` for the full access/deal-terms picture this sits inside.
>
> **Deal confirmed Sep 15:** Cynthia confirmed Reggae Pot follows the same deal as Nakhon Luang — $1/online order, 1,000 minimum / 1,500 ideal target, redesign-first-then-SEO sequencing. The hero now includes the three exact conversion phrases named in the original Aug 10 action plan ("Skip the line / No wait / More convenient") as a benefit strip under the Order Online buttons. That plan also calls the **menu page** the highest-intent page deserving special attention — logical next build, not done yet.

---

## What this fixes, directly

Every change here maps to a specific, verified finding in `01-Website-Review/RPJG-Website-Review-2026-09-03.md`:

| Audit finding | Fix in this prototype |
|---|---|
| Hero renders as a blank white box on every device (broken 2021 Slider Revolution plugin, `Uncaught Can not detect viewport width`) | Hero is pure CSS/HTML. No slider, no JS dependency, nothing that can throw a viewport-detection error. Verified in browser at desktop and 375×812 mobile — renders every time. |
| No order button visible until 4,385px down a 7,466px page on mobile (59% scroll) | A sticky bottom order bar with two buttons (Centennial / Denver) is fixed on screen at all times below 768px width. Verified: visible at scroll position 0, before any scrolling happens. |
| 11 order-related links, 7 destinations, 2 dead `#` links | Every "Order Online" link on this page points to exactly one of two real destinations: `/order/centennial/` or `/order/denver/`. Checked programmatically — 29 links, 0 dead `#` links. |
| Hours hidden behind a collapsed accordion | Hours are shown in plain text in three places (hero card, locations section, footer), no click required. |
| Centennial Sunday hours published as "11pm–7pm" (impossible) | Not repeated here. Flagged inline as `VERIFY` — see below. |

## Revised September 15, 2026 — matched to their real brand colors

Cynthia asked for the redesign to stay based on Reggae Pot's actual color theme, not an invented palette. I pulled the live site's real colors and one dish photo directly from `reggaepotjamaicangrill.com` (checked via computed styles on the live DOM, not eyeballed):

| Color | Hex | Where it lives on the real site |
|---|---|---|
| Green | `#0b9444` | The logo text and the header's "ORDER ONLINE" button — their actual primary action color |
| Gold | `#ffbf00` | The entire main nav bar background |
| Red | `#b50d0a` | The active/highlighted nav item ("Home") |
| Near-black | `#222222` | The top announcement bar |

That's the classic reggae/Rasta red-gold-green scheme, which lines up with the name "Reggae Pot" — not something I invented. The first version of this prototype used a forest-green/mustard/ember palette I made up before checking; this version replaces it with their real hex values. `index.html`'s `:root` block documents this with a comment.

I also pulled real assets straight off their server, all now used in `assets/`:
- `hero.jpg` — their actual hero food photo, used as the hero's poster/fallback image
- `ackee-saltfish.jpg` — a real dish photo, filling that dish card
- `logo-txt.png` + `icon.png` — **their real logo**, now in the header and footer, replacing the styled text wordmark from the first draft. Note: their real logo only says "REGGAE POT" — there's no "Jamaican Grill" in the actual mark, so I dropped the "Jamaican Grill" text I'd added next to it in the first version rather than keep inventing a lockup they don't have.

All of these are the restaurant's own existing assets, reused, not stock photography or redrawn.

## Added September 15, 2026 — hero video, Tamara's photo, two more dish photos

Cynthia asked whether the hero could use video, and to pull Tamara's real photo and more menu photos from the live site.

- **Hero is now a real, native HTML5 `<video>`** — `assets/hero-video.mp4`, pulled from the live site's own `/wp-content/uploads/2021/06/Reggae-Pot-Video.mp4`. Autoplay, muted, loop, `playsinline` (required for autoplay on mobile Safari/Chrome). `hero.jpg` stays as the `poster` and CSS fallback image, so the hero still shows something correct instantly and never depends on the video alone — same resilience principle as the rest of this build, just extended to video. Automatically pauses when scrolled out of view and resumes when scrolled back (standard practice for autoplay background video; most visitors scroll past it in seconds). Respects `prefers-reduced-motion` — the video is hidden entirely and the static photo shows instead.
  - ⚠️ **Not compressed.** The file is 12.75MB as pulled from their server — fine for this prototype, but should be compressed (a few MB, not 12+) before this goes anywhere near production. I don't have `ffmpeg` on this machine to do that myself this session.
- **Tamara's real photo** (`tamara.jpg`, from their `/about/` page) now fills the "Why Reggae Pot" portrait card, replacing that placeholder.
- **Two more real dish photos**, both cropped from a single combined photo I found on their `/about/` page (`Oxtail-Jerk-Chicken-1.png`, showing both plates on one table): `oxtail.png` and `jerk-chicken.png`. Cropped with Python/Pillow around each plate individually — each crop has a small, natural-looking sliver of the other plate visible at one corner (like two dishes photographed together on a table), not a mistake.
- **Curry Goat is still a placeholder** — no real photo of it turned up on the homepage, `/about/`, `/menu/`, or `/catering/`. Worth checking their Facebook/Instagram directly, the same way the others were found on the site itself.

**Fonts changed too, on purpose.** Their live site actually uses Poppins and Lato — both are on the generic/overused list for premium redesign work, so I kept Fraunces + Work Sans instead. Flagging this since it's a deliberate deviation from "keep everything the same," not an oversight — say the word if you'd rather match their exact fonts too.

## What's placeholder — do not ship as-is

- **Curry Goat still has no real photo** — a CSS placeholder, only one left of the four dish cards. Worth checking Facebook/Instagram for a shot.
- **The hero video needs compressing** before production — see above, 12.75MB is too heavy to ship as-is.
- **Centennial's Sunday hours are marked "VERIFY" in the code**, not stated as fact. The live site currently shows an impossible time (11pm–7pm); Session 1 guessed the intended time is 11am–7pm but that was never confirmed by the owner. Get the real number before this ships — do not guess in the final copy.
- **The two customer review quotes are real** (pulled from Session 1's ICP research, sourced from the live site's published reviews) **but are not attributed to a name or platform.** They're marked `VERIFY` in the code. Per the brand voice non-negotiables, a quote must carry the name and platform as published — pull those from the source reviews (Google or Facebook) before this ships.
- **No prices appear anywhere**, on purpose — the live menu has real pricing errors (several $0.00 items) that need fixing in Clover first.
- **No Colorado Springs mention anywhere**, on purpose — that question is still open with Magister.

## What was verified this session

- ✅ Renders correctly at desktop (1280px) and mobile (375×812) — verified over a real local server (`python -m http.server`), not just the file preview.
- ✅ Zero browser console errors, in every round of changes.
- ✅ Zero dead links (checked all 29 `<a href>` elements programmatically).
- ✅ Mobile sticky order bar confirmed visible at scroll position 0 — the direct fix for the audit's top-priority finding. Re-confirmed after every subsequent change.
- ✅ Hero video confirmed actually playing (not just present) — checked `paused`, `readyState`, `currentTime` advancing, and `error` directly on the video element, not just that the tag exists. Confirmed it pauses when scrolled out of view and resumes when scrolled back.
- ✅ All new images (Tamara, oxtail, jerk chicken) confirmed loading — checked via computed `background-image` values against their real URLs, not a visual guess.
- ❓ **Full visual re-confirmation of the mid-page sections (why/dishes/locations) after this round of changes was inconsistent** — this session's browser preview tool started timing out on scrolled screenshots partway through work, on and off, for reasons unrelated to the page itself (confirmed the page's own state — `document.visibilityState`, computed styles, console — stayed correct throughout). The hero itself and the mobile view were both visually confirmed working earlier. Worth a plain look in a real browser tab before calling the photo/video swap fully closed, since a screenshot is still worth more than a DOM check for "does this look right."

## Design choices, briefly

- **Colors:** their real green/gold/red/black, pulled live from the site — see the palette table above.
- **Type:** **Poppins + Lato — their real live fonts** (switched from an earlier Fraunces/Work Sans pairing on Sep 15, at Cynthia's request; see below).
- **No Patois** — matches the brand voice guide's default-to-none recommendation until Tamara confirms.
- **Skipped a multi-direction design exploration** (the standard process for a from-scratch brand) because the identity is already researched and locked from Session 1 — this is fixing a broken execution of an existing direction, not choosing a new one. If Cynthia or Magister wants to see alternate visual directions, that's a fast follow-up, not a redo.

## Added September 15, 2026 — real fonts, torn-paper dividers, more real content, section animations

Cynthia asked for four things in one message: use their real font, add a torn-paper-style divider between sections, pull in homepage content that hadn't made it in yet, and add animation to every section.

**Fonts:** switched from Fraunces/Work Sans to **Poppins (900 weight headings, 500 weight body) + Lato** — their actual live fonts, re-checked via computed styles on the real site (`h2`/`h3` = Poppins 900, body text = Poppins 500). Applied sitewide, both pages.

**Torn-paper dividers:** a jagged, torn-edge shape sits at every section boundary on both pages (6 on the homepage, 3 on the menu page) — one shared CSS `clip-path` shape, recolored per instance to match the section it introduces, so the page reads like it's built from layered torn paper rather than flat rectangular bands. Pure CSS, no image files. **Removed in the next revision below — see why.**

## Reverted September 15, 2026 — simplified after "this looks worse," researched real references first

Cynthia said the design had gotten worse, not better, and asked me to research real Jamaican restaurant sites for inspiration before changing anything else.

**Researched two real, well-regarded examples** rather than guessing again:
- **[Miss Lily's](https://www.misslilys.com/)** (NYC/Negril/Dubai) — loud, joyful, 1970s Jamaican-dancehall-poster aesthetic: saturated solid color-block sections (a full yellow band, not just an accent), thick outlined poster typography, real candid interior/staff photography, hand-drawn logo treatment.
- **[Chubby's Jamaican Kitchen](https://chubbysjamaican.com)** (Toronto, MICHELIN-listed) — the opposite register: clean, modern, minimal nav, but carried entirely by full-bleed **real, candid, people-centered photography** — no decorative tricks standing in for content.

**What both have in common, and what this build was missing:** real photography and confident color do the work. Neither site leans on decorative effects to cover gaps — there's no equivalent of a torn-paper divider or a pulsing glow anywhere on either site.

**My diagnosis of what went wrong:** the last two rounds added decoration on top of decoration — a torn-paper edge repeated nine times sitewide, a pulsing glow on the hero button, heavier staggered animation — all at once, on top of a page that still had one dish card showing a fake gradient standing in for a missing photo. That combination reads as cluttered and unfinished, not premium, especially next to real references that stay confident and restrained everywhere except the photography itself.

**Reverted:**
- **All torn-paper dividers removed**, both pages. The zigzag `clip-path` pattern, repeated identically at every boundary, read more like a coupon-stub edge than an elegant paper tear.
- **The pulsing glow on the hero's Order button removed.** Kept the gold color and the static shadow (it still stands out against the dark green), lost the infinite animation, which read as gimmicky rather than premium next to real references.
- **The Curry Goat placeholder card redesigned.** It was a translucent gold/green gradient trying to look like a photo — the thing most likely to read as "broken." Replaced with a bold solid-gold card with the dish name in large Poppins type and an honest "Photo coming soon" label, echoing Miss Lily's confident color-block sections directly. It now looks like a deliberate design choice sitting next to the three real photo cards, not a missing asset.
- **Kept:** the subtle scroll-reveal and staggered card entrance (proven, not called out as part of the problem), the real photos/video/logo, the brand colors, and Poppins/Lato.

**Verified:** zero `.torn-edge` elements remain on either page (checked via DOM query, not a glance), the CTA button's `animationName` computed as `none`, zero console errors on both pages. Screenshot-confirmed the new Curry Goat card at mobile width — reads as an intentional bold card, not a broken one.

**More real content pulled from the live site:**
- **Vegan dishes + fresh-pressed juices** — the live homepage's "About Us" block mentions these as a real differentiator ("We offer an assortment of vegan dishes, including our famous, fresh homemade juices") that hadn't made it into this redesign yet. Added a line to the dishes section.
- **Two more real review quotes** (now 4 total, up from 2) — "The portions are amazing" and "The quality and quantity of food we received was worth every penny," both pulled from Session 1's original review research, not invented. Still unattributed pending a real name/platform, same as the first two.
- **Deliberately left out:** the live site's "breakfast, lunch and dinner" claim. Hours are 11am–8pm, which doesn't really support a breakfast claim — reads like stale boilerplate copy rather than something to carry forward. Flagging the call rather than silently dropping it.

**Animations, one per section:**
- Hero content now rises in on page load (not scroll-triggered, since it's already in view) instead of appearing instantly.
- The hero's primary Order button has a slow, quiet breathing glow — pauses on hover so the hover state stays clean.
- Dish cards, location cards, and review cards now enter in a staggered cascade (each ~0.1s after the last) instead of all fading in at once.
- The three "Why Reggae Pot" traits (Generous/Rooted/Easy) slide in one at a time.
- Everything above is skipped entirely under `prefers-reduced-motion` — checked directly, not assumed.

**Verified:** fonts, torn-edge dividers (all 6 confirmed present with correct colors), staggered card reveals, and the CTA glow all confirmed via computed styles and the browser's own state. Zero console errors on either page, checked fresh after every change. Full visual screenshots confirmed for the hero and "why" sections at desktop, and for hero + traits at mobile; a couple of mid-page sections were confirmed via computed styles rather than a fresh screenshot after this session's browser preview started timing out on scrolled captures again — the same intermittent tool issue from earlier sessions, not a page defect (page state — dead links, opacity, colors — checked and correct throughout).

## Added September 15, 2026 — the menu page, built after reviewing Nakhon Luang's dev site

Cynthia shared the sibling client's (Nakhon Luang Thai Kitchen) staging site — `bigeasytest.com/nakhonluangthaicos/wp/` — and asked me to get ideas from it. That site has **three complete alternate designs of the same menu page** built side by side: "Editorial" (story-led teaser), "Order Now" (app-style, tabs and filters), and "Field Guide" (one long page, every dish, real price, sticky jump-to-category sidebar). Reggae Pot's menu page follows the **Field Guide** pattern — it's the one that matches what the Sep 3 audit already called out as the biggest gap (the real `/menu/` page is a bare ezoo embed with zero content, no H1, no descriptions), and Reggae Pot's actual ordering happens on ezoo already, so there's no need to rebuild an "Order Now" app UI a second time.

**Every item, price, and category on this page is real** — pulled directly from Reggae Pot's own ordering system (`ezoo.app/api/reggaepotcentennial/menu`), not retyped from memory or the Sep 3 audit's manual notes. 81 items across 12 categories, all currently marked available with a real price.

**What the live catalog pull found, beyond what Session 1 already knew:**
- **56 of 169 total items (33%) are marked unavailable** in ezoo right now — three entire categories (Alcoholic Beverages, Event Menu, and all but one item in Groceries/Snacks) are effectively 100% dead. None of that is shown on this page; only available, correctly-priced items made the cut. Worth flagging to whoever gets Clover/ezoo access eventually — a customer browsing those categories in the live ordering widget today sees mostly greyed-out items.
- **The $0.00 items from the Sep 3 audit are still broken** (Guava Pineapple, Mango Passion Fruit, Sorrel Ginger juices; Red Peas w/Beef and Pumpkin Chicken soups) — still live today. Rather than either hiding these dishes entirely or repeating the $0.00 error on the new page, each gets an honest callout instead ("ask your server, or call ahead") so the page doesn't look broken and doesn't pretend these dishes don't exist.
- **Two more zero-price items not previously flagged**: a $0.00 "Gift card" and a mystery $0.00 "open" item sitting in an uncategorized bucket — looks like leftover test data in the catalog. Worth mentioning if anyone gets Clover access.
- **Each category has an "Order this category ▸" link** straight to that category's anchor in the live ezoo ordering widget (`ezoo.app/reggaepotcentennial#cat-...`) — the same pattern Nakhon Luang's site uses to cut the distance between browsing and ordering.

**Scope call:** prices shown are Centennial's (same location Session 1 used as the reference, since Denver runs a separate ezoo catalog under a different slug and pulling both would roughly double this task). The page says so plainly and links each location's own Order Online button.

**Descriptions:** written for the 16 entrée-level dishes in "Reggae Pot Meals" (four reuse the exact wording already on the homepage, for consistency) plus a handful of starters/salads. Simple categories — sides, drinks, patties, pastries — get name and price only, no forced description, matching how Nakhon Luang's own Field Guide page treats simple items. One item, "Leighton's Special," has no description anywhere I could find — left blank rather than guessed at.

## Revised September 15, 2026 — font reverted, sections reordered, bigger dish photos, more real content

Cynthia asked for four more things on the homepage: bring the font back to what it was before Poppins/Lato, move the Menu/Dishes section to come right after the hero (with the Why/Tamara section moved down after it), make the dish photos bigger, and add more of the live site's own content.

**Font reverted to Fraunces + Work Sans** — back from the Poppins/Lato pairing that matched the live site exactly. Applied sitewide, both pages, including the small overrides (hero-card label, trait marks, the Curry Goat card's type treatment) that had switched to Poppins along with everything else.

**Homepage order changed** to Hero → Dishes ("The dishes people come back for") → Why Reggae Pot / Tamara → Locations → Reviews → Final CTA → Footer. The Dishes section now gets the second-best real estate on the page, right after the hero.

**Dish photos are bigger.** The grid went from 4 columns to 2, and each photo from a 4:3 rectangle to a full 1:1 square — each card is now roughly twice the size it was, so the food is the first thing that reads, not competing with three other small photos in a row. Text inside each card (dish name, the Curry Goat card's bold type treatment) scaled up to match.

**More real content from the live site:**
- Hero eyebrow now reads **"Colorado's Favorite Jamaican Restaurant · Centennial & Denver"** — pulled directly from the live site's own top announcement bar, not something I wrote.
- **Added a fourth trait, "Lively,"** to the Why section: reggae music, a game always on, a warm and colorful family-friendly room — straight from the live homepage's own "Good Vibes" intro copy, which hadn't made it into any version of this redesign until now.

**Verified:** grid computed to 2 columns at 552px each (not 4), photo `aspect-ratio` computed as `1 / 1`, `h1` font-family computed as `Fraunces, Georgia, serif` on both pages, dishes section confirmed as the first section after the hero in document order, zero console errors on either page. Screenshot-confirmed the reordered dishes section and the enlarged Curry Goat card at mobile width.

## Revised September 15, 2026 — Curry Goat swapped for a real photo, more live-site content

Cynthia said she'd asked for more live-site content and pointed out Curry Goat still had no photo — asked me to find another one of their best-selling dishes that does have a real photo, instead of the styled placeholder card.

**Found two more real dish photos** by re-scanning the live site's full HTML for every image reference, not just what had surfaced in earlier passes: `Jerk-Ribs-Reggae-Pot.jpg` and `Jerk-Wings-Reggae-Pot.jpg`. **Jerk BBQ Ribs now replaces Curry Goat's card** — it's a real, available, $22.50 menu item (confirmed in the Sep 15 ezoo pull) with a genuinely appetizing real photo. All four dish cards now show real food, zero placeholder cards. Curry Goat is still mentioned in the hero copy and meta description (it's a real, available dish) — it just isn't one of the four showcased with its own photo anymore.

**More live-site content added, since the earlier pass was too thin:**
- **Curry chicken** now gets a mention in the dishes section intro — it's named twice on the live site as a specialty dish, and hadn't made it in anywhere yet.
- **A dine-in line added to the Locations section**: "Dine in for the reggae music and the full spread, or order ahead and skip straight to eating." The live site is clearly built for dine-in too ("Join us, stay a while..."), and the Locations section previously only talked about ordering ahead — this brings the two together without undercutting the online-order priority.

**Not used, `jerk-wings.jpg` and a kitchen-in-progress shot (`Reggae-Pot-photo.jpg`)** — both downloaded and reviewed, kept in `assets/` in case they're useful for the menu page or a future section, not forced into this pass since four strong photo cards was the goal, not six.

**Verified:** all four dish-card background-images confirmed loading via computed style checks, zero console errors, Jerk BBQ Ribs card and the new Locations copy both screenshot-confirmed at mobile width.

## Revised September 15, 2026 — live site's own copy added verbatim, not paraphrased

Cynthia asked directly why the live site's content wasn't being added — turned out the gap was that I'd been extracting facts and rewriting them in the new brand voice, when what she wanted was the actual paragraphs from the live site, close to word-for-word. Asked her directly rather than guess a fourth time; she confirmed: full text blocks, near-verbatim.

**Four of the live site's own copy blocks are now in the page, essentially as written:**
- The "Good Vibes" atmosphere paragraph ("When you walk into Reggae Pot Jamaican Grill, you're greeted by pleasant, friendly and cool-as-can-be staff...") — now sits in the Why section.
- The "About Us" dish-list paragraph ("Drawing from the diverse Jamaican cuisine, our menu offers island specialties like jerk chicken, escoveitch fish, oxtail, curried goat and curry chicken...") — same section.
- The "Flavors of Jamaica" invitation paragraph ("Visit Reggae Pot Jamaican Grill for a culinary getaway to the island of Jamaica...") — same section.
- The "Jamaican Specialties" paragraph ("At Reggae Pot Jamaican Grill, you can enjoy traditional dishes such as Ackee and Salt Fish, Stewed Oxtails and Curry Chicken...") — now in the Dishes section.
- The "Order Online" paragraph ("Order your favorites ahead of time right from your phone!...") — now in the final CTA section.

**One factual edit, not a style edit, flagged plainly:** the Flavors of Jamaica paragraph originally says "local favorite for breakfast, lunch and dinner." Dropped "breakfast" — hours are 11am–8pm, so the claim doesn't hold up. Everything else in these five blocks is their own wording, not rewritten, including phrases the Sep 3 brand voice research had flagged as generic ("culinary getaway," "seasoned to perfection") — Cynthia's direct instruction here overrides that earlier guidance, and that tension is worth knowing about if this goes further, not something to quietly resolve one way or the other on my own.

**Verified:** all five text blocks present in the page and matched against the live site's actual current copy (re-checked live, not from memory), zero console errors, screenshot-confirmed at mobile width.

## Revised September 15, 2026 — each live-site content block now has its own section

Cynthia corrected the last revision: the five verbatim paragraphs shouldn't have been stuffed into existing sections as extra unlabeled text — each one needed its own section, matching how they exist as distinct blocks on the live site.

**Pulled the five paragraphs back out of Why, Dishes, and the final CTA section, and gave each one a real, standalone `<section>`** with the live site's own kicker + heading, in the order they'd naturally fall as a visitor scrolls:

1. **Good Vibes / Reggae Pot** — the atmosphere paragraph, right after the hero.
2. **Great Food / Jamaican Grill** — the About Us dish-list paragraph, after Dishes.
3. **Authentic & Delicious / Flavors of Jamaica in the Heart of Colorado** — right after that.
4. **Delicious / Jamaican Specialties** — after the Why/Tamara section.
5. **Fast & Easy / Order Online** — its own section with its own Order Online buttons, right before the final CTA band.

Built one reusable `.copy-block` section style (centered kicker + heading + paragraph, alternating cream/dark-green background for rhythm) so all five read as a consistent family of sections rather than five one-off designs.

**Verified:** all 5 `.copy-block` sections confirmed present with the correct headings via a DOM query (not a glance), zero console errors, screenshot-confirmed the section-by-section flow and color alternation at mobile width.

## Revised September 15, 2026 — the five new sections got real photo backgrounds

Cynthia flagged the five new sections (screenshots attached) as flat and empty — four nearly-identical centered-text blocks in a row, lots of padding around short text, nothing to actually look at. Fair read: same problem as the earlier "dead space" fix, just reintroduced in new sections.

**Four of the five now use a real, section-specific photo as the background** instead of a flat color panel, under the same dark-green scrim treatment as the hero (so text stays legible on any photo):
- **Good Vibes** → `reggae-pot-photo.jpg` (the kitchen-in-action shot, previously unused)
- **Jamaican Grill** → `jerk-wings.jpg` (previously unused)
- **Flavors of Jamaica** → `hero.jpg` (reused, different crop/position than the actual hero)
- **Jamaican Specialties** → `ackee-saltfish.jpg` — a direct content match, since the paragraph names Ackee and Salt Fish specifically

**Order Online stays a flat dark-green panel, on purpose** — it's the transactional section right before the final CTA, and giving every single section a photo would trade one monotony (flat color) for another (photo fatigue). One plain section in the run gives the eye somewhere to rest.

**Verified:** all four `copy-block--photo` sections confirmed rendering their assigned image via computed `background-image`, zero console errors, screenshot-confirmed at both mobile and desktop widths — text legible over every photo, no contrast issues.

## Revised September 15, 2026 — fixed the visible seam between stacked photo sections

Cynthia sent two annotated screenshots (red boxes) flagging an ugly seam where sections joined: hero → Good Vibes, and Jamaican Grill → Flavors of Jamaica.

**Root cause:** the hero and every `.copy-block--photo` section used a diagonal dark-scrim gradient (dark top-left, fading to only ~55% opacity at the bottom). That made the *bottom* edge of one photo section noticeably brighter/more photo-visible than the *top* edge of the next one (which started back at ~90% dark) — an abrupt brightness jump exactly at the section boundary, worse whenever the two photos themselves had unrelated colors (e.g. jerk wings into a hero shot).

**Fix:** changed the scrim on both `.hero::before` and `.copy-block--photo::before` from a diagonal gradient to a vertical vignette — dark (~92–96% opacity of `--green-deep`, `#0a2a1a`) at the very top and very bottom edge of every photo section, lighter (~68–74%) through the middle where the text sits. Every photo section now starts and ends at nearly the same solid dark-green tone regardless of which photo is behind it, so:
- two stacked photo sections meet at matching opacity (no more brightness jump)
- a photo section meeting a flat `--green-deep` section (`.dishes`, `.copy-block--dark`) also matches, since that's the same hex

Changed in `assets/site.css` only — no HTML changes, no new assets.

**Verified:** confirmed via `getComputedStyle` that all three `.copy-block--photo` sections and the hero now resolve to the same edge-opacity gradient shape (~0.92–0.96 at both ends). ❓ **Could not get a visual screenshot this round** — the Browser tool's screenshot came back blank/timed-out on every attempt after scrolling (the same tool flakiness noted earlier in this project; confirmed it's a tool/window-focus issue, not a page error — page loaded fine, zero console errors, correct scroll position). **What would settle it for certain:** open `index.html` yourself and look at the hero→Good Vibes and Jamaican Grill→Flavors-of-Jamaica joins directly — please confirm the seam is actually gone before this is called done.

## Revised September 15, 2026 — the seam fix wasn't enough, redesigned the section instead

Cynthia said the gradient tweak above still looked the same and to redesign it, not patch it.

Fair — tuning the scrim's opacity balanced the edges, but it didn't fix what was actually wrong: four sections in a row that are full-bleed photo banners with dark text overlays, stacked directly on each other, will always read as "glued together" banner ads no matter how well the edges match. That's a structural problem, not a color problem.

**New design for these four sections (Good Vibes, Jamaican Grill, Flavors of Jamaica, Jamaican Specialties):** dropped the full-bleed photo-background treatment entirely. Each one is now a plain cream/cream-deep section (same as the rest of the page) with the photo as a **contained, rounded card next to the text** — image and text side by side on desktop, stacked on mobile. This is the exact same pattern the "Why Reggae Pot / Tamara" section already used further down the page, just applied consistently to these four:
- **Good Vibes** — image left, text right, cream background
- **Jamaican Grill** — image right, text left, cream-deep background
- **Flavors of Jamaica** — image left, text right, cream background
- **Jamaican Specialties** — image right, text left, cream-deep background

Alternating the image side and the background tint keeps four sections in a row from reading as one repeated block, without needing torn-paper dividers or glow effects (both already ruled out earlier).

**Why this actually fixes the seam, structurally:** there is no longer any full-bleed edge-to-edge photo anywhere in this run of sections — so there's no photo edge left to clash with the next section's photo edge. The hero (still a full-bleed dark photo) now hands off directly into a plain cream section, which is a completely normal, common dark-to-light section transition, not two photo banners meeting.

Removed the now-unused `.copy-block--photo` CSS entirely rather than leave dead code behind.

**Verified:** ✅ confirmed via DOM query that all four sections carry the correct classes, background tint, alternating image side, and correct photo per section. ✅ Screenshot-confirmed the hero → Good Vibes boundary directly — clean cream-to-hero transition, no seam. ❓ **Could not get a screenshot of the Jamaican Grill → Flavors of Jamaica boundary specifically** — the Browser tool went blank on every scroll attempt after the first screenshot (same recurring tool flakiness, not a page problem — confirmed the page itself loads and scrolls correctly via JS checks). Since both sections use the identical new pattern verified working at the first boundary, and neither has a full-bleed photo edge anymore, I'm confident this one is fixed too, but haven't seen it directly. **What would settle it for certain:** please open `index.html` and scroll past the Jamaican Grill section specifically to confirm.

## Revised September 15, 2026 — three targeted fixes from screenshots

Cynthia sent three annotated screenshots with specific, separate asks:

**1. Flip Flavors of Jamaica's image/text sides.** Done — but while wiring this up I found a real bug: the `.reverse` CSS rule was targeting the wrong element (`.content-split.reverse` instead of `.split-grid.reverse`, since the `reverse` class actually sits on the inner wrap div), so it never matched anything. That means **Jamaican Grill and Jamaican Specialties had also been silently rendering image-left this whole time**, not image-right as I'd reported verified last round — my verification check only confirmed the class existed in the HTML, not that the CSS rule actually applied. Fixed the selector, so both of those now correctly render image-right as originally designed. Combined with flipping Flavors to image-right as asked, that put three sections in a row (Jamaican Grill, Flavors, Why) all image-right — so I also un-reversed Jamaican Specialties (back to image-left) to restore some rhythm at the tail end: Good Vibes(L) → Jamaican Grill(R) → Flavors(R) → Why(R) → Jamaican Specialties(L). Flagging this rather than silently deciding it — if you want a different arrangement, say which section should flip.

**2. Green background on the Why/Tamara section.** Done — `#why` now uses `--green-deep` (same dark green as Dishes/Order Online), with all its text, the eyebrow, and the trait icons recolored for contrast against it (white headings, gold eyebrow/icons instead of green/red, matching the pattern already used elsewhere on dark sections). This was blending into Flavors of Jamaica above it (both were cream) with no visual break.

**3. Locations hours — match the live site exactly, no on-page note.** Re-pulled the live site's actual location page (`reggaepotjamaicangrill.com`, checked live, not from memory) and both cards now show the real 3-tier schedule exactly as published: Mon–Thu 11am–8pm, Fri–Sat 11am–9pm, and Sunday (Centennial: 11pm–7pm · Denver: Closed). Removed the red `.loc-verify` warning box and its CSS rule entirely, per instruction.

**Flagging separately, not as an on-page note per instruction:** Centennial's live-site Sunday hours ("11pm–7pm") are almost certainly a typo — a close time before an open time isn't a valid range, most likely meant to be 11am–7pm. This prototype now shows it exactly as published, matching the ask, but it should get corrected at the source before this goes live anywhere real. Also worth knowing: the hero section's own mini location card (top of the page) still shows the older simplified "Mon–Sat 11am–8pm" format — it wasn't part of any of the three screenshots, so I left it alone rather than guess you wanted it changed too; say the word if you want it to match the new 3-line format.

**Verified:** ✅ all three changes confirmed via computed styles and DOM text content (image-side order, `#why` background/text colors, exact hours text on both cards, `.loc-verify` confirmed removed), zero console errors. ✅ Screenshot-confirmed the hero/top-of-page render correctly. ❓ Could not get a screenshot further down the page this round (same recurring Browser-tool flakiness after scrolling, not a page issue) — please give this one a look yourself before calling it done.

## Revised September 15, 2026 — only Flavors of Jamaica should have flipped

Cynthia corrected the rebalancing above: only the Flavors of Jamaica section was supposed to change sides — Jamaican Grill should stay exactly as it looked before (image left), not flip to image-right just because my earlier bug fix made that technically "correct" per the original design intent.

**Reverted Jamaican Grill back to image-left**, removing the `reverse` class I'd fixed it to use. Left a comment in the HTML explaining this is intentional so it doesn't get "corrected" again by mistake later. Jamaican Specialties stays image-left too (already set that way last round). Current state: Good Vibes(left) → Jamaican Grill(left) → **Flavors of Jamaica(right — the only one that changed)** → Why(right, unchanged) → Jamaican Specialties(left).

**Verified:** ✅ computed styles confirm exactly one of the four sections (Flavors of Jamaica) has its image on the right; the other three are left, matching Cynthia's direct instruction. ❓ Could not get a visual screenshot this round (same Browser-tool flakiness after scrolling) — the computed-style check is solid, but please confirm visually.

## Revised September 15, 2026 — Order Online and Final CTA were too plain

Cynthia sent two screenshots of the bottom two sections and said to redesign them, too simple. Fair — both were just centered kicker/heading/paragraph/two-buttons, nearly identical in shape to each other, back to back.

**Order Online** (dark green, live-site verbatim copy) — added the same "Skip the line · No wait · More convenient than calling" benefit checklist already used in the hero, between the paragraph and the buttons. Real conversion language already established elsewhere on the page, not new copy, so this section now has something to actually read instead of two lines of text.

**Final CTA** — rebuilt from centered text into the same photo-card-next-to-text layout used for Good Vibes/Jamaican Grill/etc. above (text left, a real photo — the Jerk BBQ Ribs shot — in a rounded card on the right), still on its gold background. This makes the very last section before the footer a real photo instead of a third flat-color panel in a row, and visually differentiates it from Order Online right above it (icon list vs. photo).

Generalized the `.split-grid`/`.split-media` CSS so it's no longer tied to `.content-split` — Final CTA now reuses the exact same grid system rather than a separate one-off layout.

**Verified:** ✅ DOM-confirmed the benefit list renders with the right 3 items under Order Online, confirmed Final CTA's `.split-grid`/`.split-media` structure and correct photo, zero console errors, confirmed via `find` that both sections' text renders in the accessibility tree (not blank). ❓ **No visual screenshot this round** — same recurring Browser-tool flakiness on scroll (confirmed it's the tool: content is present and correctly structured per every other check, just couldn't get a rendered image this time). Please look at both sections directly before calling this done.

## Revised September 15, 2026 — dead space above the dish grid

Cynthia's screenshot showed a big empty rectangle to the right of the "The dishes people come back for" heading — the intro text sat alone on the left of a full-width dark section with nothing on the right.

**Fixed by moving the "View the full menu ▸" link up there**, opposite the heading, instead of leaving it at the bottom of the section where it was. Real element, not decoration — no new copy invented. Removed the duplicate link that used to sit below the dish grid. Stacks on mobile.

**Verified:** ✅ DOM/computed-style confirmed the new `.dishes-head` flex row renders correctly (heading block left, button right), confirmed the old bottom link is gone, zero console errors. ❓ No screenshot this round — same recurring Browser-tool flakiness after scrolling. Please check visually.

## Revised September 15, 2026 — an Order Online CTA in every section

Cynthia asked for an order button in every section, not just the ones that already had one (Hero, Locations, Order Online, Final CTA, header, mobile sticky bar, footer).

**Added a small "Order Online ▸" link to every remaining content section**: Good Vibes, Dishes (next to the existing "View full menu" link), Jamaican Grill, Flavors of Jamaica, Why/Tamara, Jamaican Specialties, and Reviews. Kept these lightweight — a single small outline button (`.btn-sm`), not a repeat of the full two-location button pair — pointing to `#locations` so the visitor picks Centennial or Denver there rather than every section duplicating both location links. The sections that already had explicit per-location buttons (Hero, Locations, Order Online, Final CTA) were left as they were.

**Verified:** ✅ programmatically confirmed all 11 content sections now contain at least one order-related link (checked via DOM query counting links with "order" in the text or href), zero console errors, top-of-page screenshot-confirmed clean.

## Revised September 15, 2026 — each new CTA needed both locations, not one generic link

Cynthia corrected the CTA rollout above: the "Order Online ▸" link I'd added to each section pointed to `#locations` (scroll down and pick) — she wants the real per-location buttons ("Order Online — Centennial" / "Order Online — Denver") in every section, matching the pattern already used in Hero/Locations/Order Online/Final CTA.

**Swapped all 7 new single links for the actual two-button pair** (`/order/centennial/` and `/order/denver/` directly, no more `#locations` scroll-jump), sized down (`.btn-sm`) to stay proportionate inside each section. Dishes section now has three buttons in its header row (Order — Centennial, Order — Denver, View full menu) since it already had the menu link from the dead-space fix; confirmed via DOM measurement it doesn't overflow even at 375px mobile width.

**Verified:** ✅ programmatically confirmed all 11 content sections now have both a `/order/centennial/` and `/order/denver/` link (11 for 11), zero console errors, mobile-width (375px) screenshot-confirmed the hero and Good Vibes sections render correctly with no horizontal scroll. ❓ One mobile screenshot of the Dishes section's 3-button row appeared visually clipped, but I double-checked with `getBoundingClientRect`/`scrollWidth` and confirmed there is **no actual overflow** — every element's right edge sits at 351px inside a 375px viewport. Treating that screenshot as a capture artifact (this tool has been unreliable all session), not a real bug — but flagging it here in case you spot something different when you look yourself.

## Revised September 15, 2026 — "View the full menu" wasn't aligned under the order buttons

Cynthia's screenshot showed "View the full menu" sitting oddly next to/under just the Denver button instead of evenly below the pair. Changed the button-group container from right-aligned (`align-items:flex-end`) to stretched (`align-items:stretch`), and let "View the full menu" fill that stretched width — it now matches the Centennial/Denver row's width and position exactly, sitting cleanly on its own line beneath it.

**Verified:** ✅ `getBoundingClientRect` confirms both rows now share the exact same width (429.9px) and left edge (x:24), zero console errors. ❓ No screenshot this round (same recurring tool flakiness) — the measurement is exact, but take a look yourself when you can.

## Revised September 17, 2026 — removed every em-dash from visible content

Cynthia flagged too many em-dashes in the published content. Went through every visible piece of text on both pages (headings, paragraphs, button labels, meta title/description, footer note, review citations) and replaced each em-dash with whatever reads naturally in context, no fixed formula:

- Button labels ("Order Online — Centennial") → colon ("Order Online: Centennial"), matching the header/mobile-bar's existing "Order: Centennial" style
- Joining two clauses → comma, period, or colon depending on the relationship (e.g. "off the grill — seasoned with..." → "off the grill, seasoned with...")
- Review citations ("— Reggae Pot customer review") → dropped the dash entirely, the `<cite>` styling already sets it apart
- `<title>` tag → em-dash swapped for a pipe, the standard SEO title separator
- Byline ("owner & lead chef — Montego Bay, Jamaica") → "owner & lead chef, from Montego Bay, Jamaica"

**One correction worth flagging:** the Flavors of Jamaica paragraph is one of the live-site verbatim blocks, and the live site itself actually uses an em-dash mid-sentence ("...island of Jamaica — right in the heart of Colorado"). I replaced it with a comma per this instruction — small punctuation deviation from strict verbatim, but the wording itself is untouched, and while re-checking that sentence against the live site I noticed the *next* clause on the live site actually uses a period + "Or," (not an em-dash like this prototype had) — fixed that to match the live site exactly as a bonus, since it was wrong either way.

Left em-dashes alone in two places that aren't visitor-facing: my own HTML comments (dev notes to whoever picks up this code next) and the CSS file's comments. Neither renders on the page.

**Verified:** ✅ ran a live DOM text-content check on both pages after the changes (`document.body.innerText.includes('—')`) — confirmed **zero** em-dashes in what a visitor actually sees, on both index.html and menu/index.html. Zero console errors, screenshot-confirmed the menu page renders cleanly.

## Revised September 18, 2026 — applied Brian's standing design requirements

Cynthia shared internal Slack/Basecamp context: Brian (CEO) has standing requirements that apply to **every** Magister restaurant redesign, not just the one they were originally written for. Audited this prototype against them directly.

**Brian's standing requirements:**
1. Always include a Home page with a visible Home nav link
2. "Contact" not "Contact Us" — n/a here, this prototype has no Contact link at all currently
3. No cursive fonts, especially in reviews — ✅ already compliant, verified: no cursive font-family anywhere, review quotes use italic Fraunces (a serif), not a script font
4. **Order Online CTA prominent, and the same button color throughout**

**What was actually wrong (#4):** the primary "Order Online" button was gold inside the hero and most content sections, but plain green in the header's Centennial button, the Locations cards, and the Final CTA section (which used an inline-style override) — three different treatments for what should read as one consistent action.

**Fixed:**
- Added an explicit **Home** link, first item in the nav.
- Made gold the one consistent primary-button color sitewide (was previously gold only inside a scoped selector, green everywhere else by default).
- Fixed the header: Centennial is now the solid gold button, Denver the outline one — matching the pattern used in every other section (previously reversed).
- Fixed the Final CTA section: its button now uses the exact same gold fill and text color as every other Order Online button on the site. That section's background is also gold, so a plain gold-on-gold button would vanish — gave it a dark border there for definition, without changing the button's actual color.

**Flagging, not changing without your say-so:** Brian's CRO notes (from the referenced Basecamp threads) also call out "No Wait" as an unsupported promise to avoid — this prototype's hero and Order Online benefit list both include "No wait." That exact phrase was something you explicitly asked me to add earlier this session, sourced from the original Aug 10 action plan, so I didn't touch it without checking with you first. Let me know if you want it softened (e.g. to "Order ahead") or left as is.

**Verified:** ✅ confirmed via computed styles that all 13 primary Order Online buttons on the page now resolve to the exact same background color, zero console errors, screenshot-confirmed the header and the Final CTA section both render correctly with the fix.

## Revised September 18, 2026 — periods in headings

Cynthia flagged that item #1 from Beth's Slack list of "obviously-AI-design" tells (periods in headers) was still present — the previous round only covered Brian's 4-point standing list, not this earlier, separate feedback from the same thread. Went through every `<h1>`/`<h2>` on both pages and removed every period:

- "Real Jamaican food, cooked like home**.**" → "Real Jamaican food, cooked like home"
- "South Denver metro**.** Worth the drive**.**" → "South Denver metro, worth the drive"
- "Tamara Nisbeth learned to cook in Montego Bay**.** She cooks the same way here**.**" → "Tamara Nisbeth learned to cook in Montego Bay, and cooks the same way here"
- "Skip the line**.** Ready when you get here**.**" → "Skip the line, ready when you get here" (this one also appears on the menu page — fixed there too)

**Verified:** ✅ searched every `<h1>`/`<h2>` on both `index.html` and `menu/index.html` for a literal period — zero remain. Confirmed the resulting heading text directly via `textContent` (not just the source), zero console errors, screenshot-confirmed the hero heading renders correctly.

## Not done yet

- The other 6 pages (order/centennial, order/denver, about, catering, locations) — homepage and menu are the two pages built so far.
- Nothing has been connected to WordPress. Per Beth's Sep 14 comment, hosting is portal.ivywildmedia.com and **no new WP backend users** — so implementation needs to go through whoever already has that access (David/Richard/Durga's team), not through a new login.
- Confirmed Sunday hours for Centennial.
- Named, platform-attributed review quotes.
- Denver's own menu/pricing, if it turns out to meaningfully differ from Centennial's.
