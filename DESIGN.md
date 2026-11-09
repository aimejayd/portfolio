# DESIGN.md — JayD Portfolio

> Design system for Jean De Dieu Manishimwe's personal portfolio. Any AI agent or developer changing the site should read this first and follow it exactly.

---

## 1. Visual Theme & Atmosphere

**Mood:** Intelligent, calm, premium, quietly futuristic. A dark night-sky canvas where a living neural network drifts behind frosted-glass panels. It should feel like the interface of a well-built AI product, not a template.

**Personality keywords:** engineered · confident · human · AI-native · outcome-focused

**Signature elements (never remove):**
1. **Neural-network canvas** — slow-drifting nodes connected by faint violet lines; lines turn teal and reach toward the cursor.
2. **The Orb** — a pulsing gradient sphere that represents the "JayD" identity (logo, chat avatar).
3. **Tri-colour gradient** — violet → teal → pink, used sparingly for emphasis words, meters and accents.
4. **Glass panels** — translucent cards with blur, hairline borders and a cursor-following violet glow.
5. **JayD assistant** — the chat interface in the hero is the centrepiece; the site "talks".
6. **Mono annotations** — `// 01 — Section` labels, `epoch`/`> prompt` style microcopy in JetBrains Mono.

**Content philosophy:** Outcomes, not a CV. Show capabilities and impact (engineering, leadership, product, project delivery, security, AI). Do **not** list employers or dated job history — that belongs in the downloadable CV.

---

## 2. Colour Palette & Roles

| Token | Value | Role |
|---|---|---|
| `--bg` | `#06060C` | Page background (near-black with blue undertone) |
| `--panel` | `rgba(18,18,32,.62)` | Glass card fill (always with `backdrop-filter: blur(14px)`) |
| `--panel-solid` | `#101020` | Opaque surfaces: modals, command palette |
| `--line` | `rgba(255,255,255,.08)` | Hairline borders, dividers |
| `--text` | `#ECEBFF` | Primary text (lavender-tinted white) |
| `--muted` | `#9A98B8` | Body copy, descriptions |
| `--dim` | `#5F5D7D` | Labels, metadata, footer |
| `--v` (Violet) | `#8B5CF6` | Primary accent — AI, focus, active states |
| `--c` (Teal) | `#2DD4BF` | Secondary accent — status, "live", eyebrow labels, links |
| `--p` (Pink) | `#F472B6` | Tertiary — gradient tail, decorative glows only |
| `--grad` | `linear-gradient(120deg, #8B5CF6 0%, #2DD4BF 55%, #F472B6 100%)` | Signature gradient |

**Usage rules**
- ~85% of the screen is `--bg` + glass. Accents are scarce and meaningful.
- Gradient text max **once per section** (usually the last line/word of a heading).
- Teal = "alive" (status dots, online, tagline labels). Violet = "interactive" (hover, focus, active nav, user chat bubble).
- Pink is never used for text or UI states on its own.
- Tinted fills use the accent at 6–18% alpha (e.g. `rgba(139,92,246,.1)` for tags, `.18` for active nav).
- Ambient glows: violet blob top-left (28% opacity), teal blob bottom-right (18%), both `blur(120px)`, fixed.

---

## 3. Typography

| Role | Font | Weight | Size | Tracking | Line-height |
|---|---|---|---|---|---|
| Display (H1) | Space Grotesk | 700 | `clamp(2.6rem, 6.2vw, 5rem)` | `-0.045em` | 0.98 |
| Section (H2) | Space Grotesk | 700 | `clamp(2rem, 4.4vw, 3.2rem)` | `-0.035em` | 1.02 |
| Card title (H3) | Space Grotesk | 600–700 | 1.1–1.5rem | `-0.01 to -0.02em` | 1.3 |
| Lead | Space Grotesk | 400 | 1.12rem | 0 | 1.55 |
| Body | Space Grotesk | 400 | 0.9–0.95rem | 0 | 1.55 |
| Eyebrow / label | JetBrains Mono | 400–500 | 0.72–0.78rem | `0.08–0.1em`, UPPERCASE | — |
| Code / microcopy | JetBrains Mono | 400 | 0.72–0.9rem | 0 | — |

- Load: `Space Grotesk 400/500/600/700`, `JetBrains Mono 400/500` (Google Fonts).
- Headings are tight and big; body is quiet and `--muted`. Emphasis inside body uses `--text` at weight 500, not bold colour.
- Headlines use short punchy lines with manual `<br>` breaks; final line often gradient.
- Eyebrow pattern: `// 0N — Name` in teal mono.

---

## 4. Components

### Buttons
- **Primary (`.btn-a`)**: bg `--text`, text `#0A0A14`, radius 14px, padding `13px 22px`, weight 600. Hover: `translateY(-2px)` + violet glow shadow `0 12px 40px -10px rgba(139,92,246,.8)`.
- **Secondary (`.btn-b`)**: glass fill, `--line` border, `--text`. Hover: border → teal 50%.
- Arrows in labels: `→` (in-page), `↗` (external), `↓` (download).
- Max one primary button per group.

### Glass card (`.glass`)
- Fill `--panel`, border `1px --line`, radius `20px`, `backdrop-filter: blur(14px)`, padding 22–30px.
- Hover: radial violet spotlight follows cursor (`--mx/--my` custom props, 400px radius, 13% alpha).
- Never use solid-colour or white cards.

### Pill / status badge
- Radius 999px, mono 0.78rem, teal border 30% + teal fill 6%, with an 8px glowing teal dot.

### Tags
- Radius 8px, 0.72rem, violet fill 10%, violet border 20%, text `#C4B5FD`.

### Chat assistant (JayD)
- Wrapper: 1px gradient border (violet → teal → pink at 25–60% alpha), radius 24px, inner `rgba(10,10,22,.9)` + blur 20px.
- Header: Orb avatar (34px), name, subtitle, teal "online" indicator.
- Bot bubble: 5% white fill, hairline border, top-left radius 4px.
- User bubble: `linear-gradient(135deg, #7C3AED, #4F46E5)`, top-right radius 4px.
- Typing indicator: three bouncing dots, then character-by-character streaming (~12ms/char).
- Suggestion chips: pill, hairline border, hover → violet border.
- Input: 4% white fill, radius 12px, focus → violet border; send button uses `--grad`.

### Orb
- Circle filled with `--grad`, `box-shadow: 0 0 24px rgba(139,92,246,.7)`, 3s pulse alternating to a teal glow and `scale(1.06)`.

### Dock navigation
- Fixed, bottom-centre pill (radius 999px), `rgba(16,16,32,.75)` + blur 16px.
- Links: muted → active/hover gets violet 18% fill + `--text`. Active state tracks scroll position.

### Command palette (Ctrl/⌘ K)
- Overlay `rgba(0,0,0,.55)` + blur 6px; box `--panel-solid`, radius 18px, max-width 560px.
- Items highlight with violet 15% fill; type hints in mono `--dim`.

### Metrics
- Left border 2px using `--grad` (border-image); value 1.6rem/700; caption 0.8rem muted.

### Skill meter
- Five 14×6px segments, radius 2px; filled = `--grad`, empty = 8% white.

### Credential seal
- 64px circle, radial violet→teal fill, violet border 45%, inner + outer glow, mono label.

### Bento grid
- 6-column grid, gap 16px; feature tile spans 4, others span 2. Labels in mono uppercase `--dim`.

---

## 5. Layout Principles

- Container: `max-width: 1160px`, side padding 20px.
- Section rhythm: `padding: 110px 0 40px`. Section header = eyebrow + H2 left, short description right (max 380px).
- Grid gaps: 16px (cards), 48px (hero columns).
- Hero: two columns (`1.05fr / 1fr`) — statement left, JayD chat right; min-height near full viewport.
- Section order: Hero → Profile (bento) → Credentials → Impact → Capabilities → Selected Work → Stack → Contact.
- Asymmetric grids preferred (7/5, 4/4/4 on a 12-col) for projects; avoid uniform rows everywhere.
- Leave bottom padding (~100px) so content is never hidden behind the dock.

---

## 6. Depth & Elevation

| Level | Treatment | Used for |
|---|---|---|
| 0 | Canvas network + ambient blurred glows | Background |
| 1 | Glass `--panel` + blur 14px + hairline | Cards, sections |
| 2 | Glass + blur 16–20px + `0 20px 50px -20px #000` | Dock, chat |
| 3 | Solid `--panel-solid` + `0 30px 80px -20px #000` over dimmed overlay | Command palette / modals |

- Depth comes from blur, translucency and glow — **not** heavy drop shadows.
- Glows are coloured (violet/teal), never grey.

---

## 7. Motion

- **Reveal on scroll:** opacity 0 → 1, `translateY(30px)` → 0, 0.8s `cubic-bezier(.2,.7,.2,1)`.
- **Hover lift:** `translateY(-2px to -4px)`, 0.25s.
- **Typing effects:** role rotator in hero (type 70ms/char, delete 35ms, hold 1.7s) with blinking `▍` caret.
- **Counters:** count up on load.
- **Ambient:** orb pulse 3s, bar chart grow 2.4s alternate, network drift ~0.35px/frame.
- Always honour `prefers-reduced-motion: reduce` — disable animations and network drift.

---

## 8. Do's and Don'ts

**Do**
- Keep the AI feel through behaviour (chat, typing, network, command palette), not robot clip-art.
- Write in first person, short, confident, outcome-led ("Delivered ISO/IEC 20000 & 27001 certifications").
- Lead with breadth: software engineering, engineering leadership, product, project delivery (PMP), security (CISSP, ISO 27001), AI.
- Keep contrast ≥ 4.5:1 for body text on `--bg`.
- Use mono microcopy for system-like flavour (`// 02 — Impact`, `> Software Engineer`).

**Don't**
- Don't list employers, job dates or a CV-style timeline — link to the CV instead.
- Don't add light-mode, white cards or flat solid colour blocks.
- Don't use the gradient on body text, more than one heading per section, or large background fills.
- Don't introduce new accent colours, fonts, emoji-heavy UI, or stock "AI brain/robot" imagery.
- Don't copy another brand's identity; this system is unique to JayD.
- Don't add confidential details (internal system names, incidents, client data).

---

## 9. Responsive Behaviour

| Breakpoint | Changes |
|---|---|
| ≤ 960px | Credentials grid 4 → 2 columns |
| ≤ 900px | Hero stacks (statement above chat), min-height removed |
| ≤ 860px | Capabilities 3 → 1; Impact 3 → 2; projects full-width |
| ≤ 820px | Bento 6 → 2 columns |
| ≤ 700px | Hide Kigali clock in top bar |
| ≤ 560px | Dock links tighten (8px × 10px, 0.74rem) |
| ≤ 540px | Everything single column |

- No horizontal scroll at 360px width. Touch targets ≥ 40px.
- Network density scales with viewport area (max ~90 nodes).

---

## 10. Agent Prompt Guide

When asked to add or change something on this site:

1. Reuse existing tokens (`--bg`, `--panel`, `--v`, `--c`, `--grad`…) — never hard-code new colours.
2. New sections follow: `<section id>` → `.sh` header (`.tagline.mono` eyebrow + `h2`, optional right-side `p`) → grid of `.glass` cards with `.reveal`.
3. Add any new section to the dock nav, the command palette list, and the scroll-spy array.
4. If the content is something a visitor might ask, add a matching entry to the JayD knowledge base (keywords + first-person answer).
5. Keep everything in a single self-contained HTML file until the site is migrated to a framework.
6. Check: dark only, reduced-motion safe, mobile ≤ 390px has no overflow, no employer history.

**Example prompt:**
> "Using DESIGN.md, add a 'Writing' section after Selected Work with three glass cards for articles: mono category label, title, one-line summary, and a ↗ link. Add it to the dock, command palette and JayD."
