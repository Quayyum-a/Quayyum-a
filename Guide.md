# Profile README — Setup & Design Guide

This is the companion doc to `README.md`. It's not meant to be published on your profile — keep it in the repo (or off it entirely) as your own reference for setup and future edits.

## 1. Folder structure

```
your-github-username/            (a repo with this exact name is what GitHub renders on your profile)
├── README.md                    ← the profile page itself
├── GUIDE.md                     ← this file (optional to keep in the repo)
├── assets/
│   ├── banner.svg                ← custom hero banner (built, ready to use)
│   ├── icons/                    ← empty — see note in assets/icons/README.md
│   └── screenshots/               ← empty — see note in assets/screenshots/README.md
└── .github/
    └── workflows/
        └── snake.yml              ← generates the contribution-snake animation
```

To make this live: create a public GitHub repo with **the exact same name as your username**, and push these files to it. GitHub automatically renders that repo's `README.md` on your profile page.

## 2. Placeholder checklist (do these first)

Nothing in `README.md` was invented — every fact about your work is real, pulled from what you've actually built. The only placeholders are contact/identity details I don't have. Search the file for `USERNAME`, `your-`, `you@example.com`, and the `<!-- TODO -->` comments, and replace:

- [ ] `USERNAME` → your GitHub handle (appears in every stats/analytics URL and the profile-view counter)
- [ ] Portfolio URL
- [ ] LinkedIn handle
- [ ] Email address
- [ ] X/Twitter handle (or delete that badge if you don't want it listed)
- [ ] Calendly link (or delete that badge)
- [ ] The two "Repository: private — case study available on request" lines, once/if you decide to make any of the three repos public

## 3. Design system

**Color palette** — deliberately not the cream-and-terracotta or near-black-plus-one-accent looks that most AI-generated profiles default to. The direction here is a paper ledger rendered digitally: ink-navy background, a ledger's ruled margin line in a muted green, warm amber for the "ink," and a teal reserved for trust/verification signals — which ties directly to UrbanFix's actual product thesis.

| Name | Hex | Used for |
|---|---|---|
| Ink Navy | `#0B0E14` | Background |
| Ledger Rule | `#16202C` | Faint ruled lines |
| Naira Green | `#0F7A4C` | Ledger margin line, gradient footer |
| Verified Teal | `#35B8A6` | Eyebrow text, "open to work" pill, accents |
| Ink Amber | `#E3A548` | Cursor blink, ink-swash signature |
| Off-White | `#E9EDF2` | Primary text |
| Muted Slate | `#9AAAC0` | Secondary/tagline text |

**Typography** — two roles, used deliberately rather than interchangeably:
- **Display / code voice:** `JetBrains Mono` (falls back to `Fira Code`, then system monospace) — used for the name, the eyebrow line, and anything meant to read as "written by an engineer."
- **Body voice:** `Inter` (falls back to system sans) — used for the tagline and anything meant to read as plain, human copy.

Custom `@font-face` imports don't reliably render in GitHub's SVG sanitizer, so both stacks fall back gracefully to system fonts — the design holds up even if a viewer's system doesn't have JetBrains Mono or Inter installed.

**Signature element:** the ledger margin rule (the green double line on the left of the banner) plus the ink-swash flourish under your name. Real ledger books use a red vertical rule to separate the margin from the entry columns — this reuses that exact convention in the palette's green instead, which is the one intentional "risk" in the design rather than a generic gradient-and-blob hero.

## 4. Banner asset

`assets/banner.svg` is hand-built, not AI-generated — it's plain SVG markup (see the file directly), so it's editable text, not a locked image. It renders natively in both GitHub's light and dark theme since it ships its own dark background rather than depending on GitHub's page background.

If you ever want to regenerate or restyle it in Figma or an AI image tool instead, here's a prompt that captures the same brief:

> A wide horizontal banner (1200×300), ink-navy background (#0B0E14), styled like a page from a paper ledger book rendered digitally. A thin double vertical rule near the left edge in deep green (#0F7A4C), like a ledger's margin line. Faint horizontal ruled lines across the whole background. Bold monospace name text in off-white, with a small amber ink-swash flourish beneath it like a pen stroke. A muted slate-blue tagline below. Two small pill-shaped tags at the bottom: a location tag and an "open to work" tag in teal. Minimal, high-contrast, no gradients, no stock icons — the feel of a well-kept ledger, not a marketing banner.

## 5. Animation assets

Two intentional animations, both restrained (per the "spend your boldness in one place" principle — the ledger motif is the one bold choice, everything else stays quiet):

1. **Blinking cursor** in the banner — a native SMIL `<animate>` on the amber cursor rect. No external dependency; it's inside `banner.svg`.
2. **Contribution snake** — `.github/workflows/snake.yml`, using the public [Platane/snk](https://github.com/Platane/snk) action. It runs on a schedule and on push, and generates an animated SVG of your contribution graph as a snake eating its way through it, published to an `output` branch. Reference it in `README.md` once it's run at least once:
   ```md
   ![Snake animation](https://raw.githubusercontent.com/USERNAME/USERNAME/output/snake.svg)
   ```
   (Not added to `README.md` by default since it needs to run once before the image exists — add the line back in after your first successful workflow run.)

The typing SVG in the header is a third animation, but it's served by an external tool (`readme-typing-svg.demolab.com`) rather than something in this repo — see the external services list below.

## 6. External services used, and why

| Service | Purpose |
|---|---|
| `readme-typing-svg.demolab.com` | Animated typing header line |
| `img.shields.io` | Contact badges (used sparingly — icons only, no counters) |
| `komarev.com/ghpvc` | Profile view counter |
| `github-readme-stats.vercel.app` | Stats card + top-languages card, themed to match the palette |
| `github-readme-activity-graph.vercel.app` | Contribution activity graph, themed to match |
| `github-readme-streak-stats.herokuapp.com` | Streak stats, themed to match |
| `github-profile-trophy.vercel.app` | Trophy case (kept inside a collapsed `<details>` so it doesn't compete with the real content) |
| `capsule-render.vercel.app` | Footer wave gradient (navy → green, matching the palette) |

All of these are free, widely used, community-run services — no API keys needed. Their one shared risk: if a service goes down or gets rate-limited, that section of the README temporarily won't render. None of them are load-bearing for the content itself.

## 7. Repository pinning strategy

Pin repos in this order of priority once you decide which of UrbanFix / Digital Ledger / Vendrix (or other work) to make public, or to open-source specific components of:
1. Whichever repo best demonstrates the "documentation before code" and "research-grounded" engineering approach the README leads with — ideally with its own well-written README, not just code.
2. This profile repo itself.
3. Any open-source contribution once you land one (OnlyDust / Drips Network work-in-progress, per the README's Open Source section).

Six pin slots total — better to leave slots empty than fill them with placeholder or inactive repos.

## 8. Mobile optimization

- The banner and all analytics images use `width="100%"` or percentage widths, not fixed pixel widths, so they scale down on narrow viewports.
- The two-column stats layout (`width="49%"` each) wraps to a single column automatically on mobile since GitHub's markdown renderer reflows `<img>` elements without a wrapping container.
- Tag/pill text inside `banner.svg` is kept short specifically so it doesn't clip when the banner is scaled down small.

## 9. Accessibility

- `banner.svg` has both a `role="img"` and a full `aria-label` describing the content, plus a `<title>` element — so screen readers get real information even though the name/tagline are rendered as SVG text, not HTML text.
- A plain-text `<h1>` and subtitle sit above the banner in `README.md` for the same reason: document structure and screen readers shouldn't depend on parsing an image.
- Every `<img>` tag has descriptive `alt` text — the footer wave is the one purely decorative image, so its `alt=""` is intentionally empty (correct practice for decorative images).
- The blinking cursor and typing SVG are the only motion on the page — both are small, contained, and non-essential to reading the content, so they shouldn't cause issues for motion-sensitive viewers, but there's no way to add a `prefers-reduced-motion` guard inside GitHub's markdown rendering. If that matters to you, the cursor animation can be removed by deleting the `<animate>` block inside `banner.svg`.

## 10. Performance

- `banner.svg` is ~2.7 KB — no raster images, no external font loading, nothing to download beyond the file itself.
- All analytics widgets are lazy by nature (they're just `<img>` tags) and cached by their respective services.
- No JavaScript anywhere in the repo except the optional GitHub Action, which runs on GitHub's infrastructure, not the viewer's browser.

## 11. Future enhancements

Ideas for later, not yet built:
- Swap the "private — case study available on request" lines for real repo links as projects go public.
- Add real product screenshots to `assets/screenshots/` and reference them in the Featured Projects section once UrbanFix/Digital Ledger have shippable UI to show.
- Once the contribution snake has run once, add its image back into `README.md`.
- If/when there's a real merged open-source PR, replace the "working through contribution paths" framing in the Open Source section with the actual outcome.
- Consider a second GitHub Action to auto-refresh the "Current Focus" section from a structured source (e.g., a `focus.json` file) if that list starts going stale.

## 12. Section-by-section explanation of README.md

| Section | Purpose |
|---|---|
| Hero (`h1` + banner + typing SVG + badges) | Establishes identity and credibility in the first five seconds |
| About | Positions you specifically — trust infrastructure and financial inclusion for Nigeria's informal economy — instead of generic "full-stack developer" language |
| Current Focus | Signals you're actively building, not just listing skills |
| How I Build | Replaces buzzword claims (Clean Architecture, SOLID, etc.) with specific, real decisions you've actually made |
| Tech Stack | Grouped by role, not a badge wall |
| Featured Projects | The evidence for everything claimed above — real architecture, real trade-offs, real status |
| Research Foundation | Shows the "why" behind UrbanFix, which most portfolios skip |
| Open Source | Honest about being in-progress rather than claiming contributions that haven't happened |
| Teaching & Content | DevRel/communication signal, backed by something you've actually made |
| GitHub Analytics | Standard recruiter-facing proof of activity |
| Setup | Small, human detail — costs nothing, adds texture |
| Let's Talk | The actual call to action — clearly states you're open to roles, with real contact paths once you fill them in |

## 13. Repo organization strategy (for the profile repo itself)

Keep this repo minimal and dedicated to the profile — don't use it to host actual project code. `README.md`, `assets/`, and `.github/workflows/` is the complete footprint; resist the urge to add more, since every extra file is something a visitor might click into and get confused by.

## 14. Maintenance checklist

Revisit on a recurring basis (quarterly is reasonable):
- [ ] Is "Current Focus" still accurate, or has the active project changed?
- [ ] Are the three Featured Projects still the right three to lead with?
- [ ] Has anything moved from private to public — update repo links accordingly
- [ ] Is the "open to work" pill (in the banner and in Let's Talk) still true? Remove it the moment it isn't.
- [ ] Do the GitHub Analytics widgets still load correctly (external services occasionally change their URL schemes)?
