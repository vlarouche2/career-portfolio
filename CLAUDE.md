# CLAUDE.md

This file guides Claude Code (and any other AI assistant) working in this repository.

## What this is

A single-file public portfolio site for **Vincent Larouche** — corporate strategy,
business intelligence, and financial analysis. It's a job-search asset: it is
linked from LinkedIn and sent directly to recruiters and hiring managers.
Everything here is `index.html` (HTML + CSS + JS inline, no build step, no
dependencies besides Google Fonts).

Visual theme: "Connecting the Dots," echoing Vincent's LinkedIn banner — an
animated network of connected nodes in the hero, and a recurring dot/node motif
used for bullets, stats, and section markers throughout.

## Design system

Keep any visual changes consistent with the system already encoded in
`index.html`'s `:root` variables and section styles. Don't introduce new
colors, fonts, or spacing scales ad hoc — extend the existing tokens.

**Palette (blue monochrome, navy base):**
| Token | Value | Use |
|---|---|---|
| `--navy-950` | `#061633` | Darkest hero/contact-panel background |
| `--navy-900` | `#071f3f` | Hero/contact gradient mid-stop |
| `--navy-800` | `#0b2a54` | Hero/contact gradient end-stop |
| `--blue-600` | `#1a5cb0` | Eyebrows, tags, links (darker accent) |
| `--blue-500` | `#2e7fd6` | Primary accent — dots, node markers, hover borders |
| `--sky-400` | `#5aa7e6` | Role line text, focus outlines |
| `--cyan-300` | `#79d0ea` | Hero tag, network canvas nodes/lines, contact tag |
| `--ink` | `#0a1f3c` | Body text on light backgrounds |
| `--muted` | `#4c5d76` | Secondary/supporting text |
| `--paper` / `--paper-2` | `#f3f7fc` / `#ffffff` | Page and card backgrounds |

**Type:**
- Display / headings and body: **Proxima Nova**, falling back to **Montserrat**
  (400–700 weight, loaded free via Google Fonts) since Proxima Nova has no
  free CDN source — it needs a licensed source (Adobe Fonts kit or
  self-hosted files) to actually render. Until one is added, the site
  renders in Montserrat.
- Mono (eyebrows, tags, labels, stats accents): **Space Mono**

**Layout & motifs:**
- Max content width `1120px` (`--maxw`), `14px` corner radius (`--radius`) on cards/panels.
- Recurring "node" dot (small blue circle with soft glow) marks stats, list
  bullets, and timeline steps — reinforces the connecting-the-dots concept.
- Sections alternate `--paper` and `--paper-2` (white) backgrounds with a
  `1px` hairline border (`--line`) between them.
- `.reveal` class + `IntersectionObserver` fades sections in on scroll;
  respects `prefers-reduced-motion`.
- Hero canvas (`#net`) draws an animated particle network on the plain navy
  gradient background (no banner image — that looked like a pasted-in
  screenshot). Nodes drift and their radius pulses (grows/shrinks)
  independently on a per-node sine cycle. ~14% of nodes are "large" beads
  (radius up to ~50px, slower drift/pulse) mixed among small ones — inspired
  by the varied large/small circles in `assets/banner.jpeg` (Vincent's
  LinkedIn banner), without reproducing the image itself. Every node,
  regardless of size, renders through the same `drawNode()` bead style: a
  fully opaque base fill (so connecting lines never show through) plus a
  soft highlight overlay for consistent glossy shading. Falls back to a
  static single-frame render (fixed mid-size dots) under reduced motion.
- Nodes actively avoid the hero copy: `measureKeepOut()` unions the tight
  rendered-text bounds (via `Range.getBoundingClientRect()`, not each
  element's full-width block box) of the avatar/tag/h1/role/lede/sub/cta-row,
  padded by 22px. New nodes don't spawn inside that box, and `avoidText()`
  bounces any drifting node off its edges each frame, so dots never render
  on top of the readable text. Re-measured on resize and once web fonts
  finish loading (text width can shift after the font swap).

**Sections (in order):** Nav → Hero → Highlights (stat nodes) → Expertise
(competency grid + tools chips) → Work (3 case studies) → Recommendations
(quote cards) → Contact → Footer.

When editing, preserve this structure and reuse existing CSS classes rather
than inventing parallel ones for the same purpose.

## Content guardrails — read before editing any copy

This site is **public** and actively linked from LinkedIn during a live job
search. Content mistakes here are not cosmetic — they can leak confidential
employer information or misrepresent Vincent's actual role to an interviewer
who will ask follow-up questions. Every edit to visible text must be checked
against these rules before it ships.

### 1. No confidential material
Never add:
- Executive names or titles from current/former employers (recommenders who
  gave permission to be named are the only exception — see the
  Recommendations section as the existing precedent).
- Verbatim internal quotes, meeting notes, or Slack/email excerpts.
- M&A codenames, deal names, or references to unannounced/internal-only
  initiatives.
- Internal-only financial figures — anything not independently confirmable
  from a public source.

### 2. Every number must trace to a public source
Only use figures that trace to **ADT's public investor relations materials**
or **Vincent's own resume**. The approved figures currently in use on the site:
- Core home-security market: **$19B → $25B by 2030**
- Adjacent market opportunity: **$20B+**
- ARR supported: **$4.3B**
- Competitors analyzed: **three $1B+ international competitors, left unnamed**
- Board-reporting metrics validated: **50+**

Do not add a new number to the page unless you can point to where it comes
from (ADT IR site/press release, or the resume). If a stat can't be sourced
publicly, cut it or generalize it (e.g., "~25% inflated forecast reconciled" is
fine because it describes Vincent's own work product, not a disclosed
internal figure).

### 3. Precise verbs only
Word choice must match Vincent's actual role in each decision — an interview
follow-up ("walk me through your role in that") must hold up.
- **Vincent's own work** (he did this himself): *owned, authored, built,
  recommended*.
- **Decisions/outcomes he contributed to but did not make** (leadership or
  someone else made the final call): *shaped, informed*.
- **Never** use *led* or *drove* for a decision Vincent did not personally
  make. Reserve stronger verbs (*led, drove*) only for work where he
  genuinely had ownership/authority over the outcome, not just influence.

Before adding or rewording any claim, ask: *would this survive Vincent
being asked to walk through it in an interview, in front of the people who
were actually in the room?* If not, revise it down to what he can defend.
