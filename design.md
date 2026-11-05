# Design system

Reusable visual language for the Abhiraj portfolio. This document describes the design decisions that should carry into a new project: palette, type, spacing, layout, imagery, components, motion, and responsive behavior.

## Design direction

- Editorial scrapbook rather than a conventional software dashboard.
- Warm, tactile, slightly imperfect, and personal.
- Large areas of quiet space; content should feel arranged on paper.
- Typewriter text supplies the technical/engineering character.
- Handwritten display text supplies the human character.
- Photography and cut-out desk objects act as collage layers, not as generic stock imagery.
- Use one warm accent sparingly. Most of the interface remains neutral.
- Prefer thin rules, small labels, restrained shadows, and small purposeful transitions.

## Core tokens

```css
:root {
  --paper: #fffaf5;
  --paper-card: #fffdf9;
  --paper-tint: #fcf8f3;
  --ink: #424044;
  --body-ink: #625d58;
  --muted: #817a72;
  --line: #e8e3dc;
  --warm-accent: #ad755b;
  --green-accent: #78866b;
  --typewriter: 'Courier Prime', monospace;
  --mono: 'DM Mono', monospace;
  --handwritten: 'Great Vibes', cursive;
  --soft-shadow: 0 12px 32px rgba(75, 58, 45, .08);
  --float-shadow: 0 20px 46px rgba(75, 58, 45, .13);
  --soft-radius: 18px;
  --section-pad: clamp(52px, 7vw, 88px);
}
```

### Supporting colors

Use these only for artwork and decorative surfaces:

| Purpose | Color |
| --- | --- |
| Peach artwork surface | `#ead7c7` |
| Peach artwork shape | `#d8a88c` |
| Sage artwork surface | `#dce0d3` |
| Sage artwork shape | `#899a7c` |
| Blue artwork surface | `#d5dce1` |
| Blue artwork shape | `#a1b0b6` |
| Focus outline | `#ad755b` or `#647c61` |
| Preloader encrypted text | `#9caa87` |

Avoid introducing bright saturated colors. Decorative colors should look faded, printed, or naturally photographed.

## Typography

Load the same font roles:

```css
@import url('https://fonts.googleapis.com/css2?family=Courier+Prime:wght@400;700&family=DM+Mono:wght@400;500&family=DM+Sans:wght@400;500;600;700&family=Great+Vibes&family=Playfair+Display:ital,wght@1,500&display=swap');
```

| Role | Font | Size / line height | Treatment |
| --- | --- | --- | --- |
| Main UI and fallback | `Courier Prime` | inherited | Technical, typewritten texture |
| Small metadata | `DM Mono` | `9–11px / 1.3–1.5` | Uppercase or compact labels, slight tracking |
| Hero name | `Great Vibes` | `clamp(72px, 6vw, 116px)` | Regular weight, centered, dark ink |
| Body copy | `Courier Prime` | `14px / 1.8` | Muted brown-gray |
| Section label | `Courier Prime` | `20px / 1.3` | Normal case, tight tracking |
| Project title | `Courier Prime` | `17px / 1.25` | Medium weight, slight negative tracking |
| About lead | `Courier Prime` | `20px / 1.55` | Dark ink, short readable measure |
| Handwritten signoff | `Great Vibes` | `32px / 1.1` | Warm accent |

Rules:

- Use `font-synthesis: none` and `text-rendering: optimizeLegibility`.
- Keep body text at a comfortable measure; the About copy is capped around `620px`.
- Use `letter-spacing: -.025em` for typewriter headings and project titles.
- Use uppercase and tracking for technical metadata, not for paragraphs.
- Do not use more than three type families in one screen: typewriter, mono, and handwritten.

## Global layout

- Background: `var(--paper)`.
- Text: `var(--body-ink)` by default, `var(--ink)` for headings.
- Horizontal content wrapper: `width: min(1100px, calc(100% - 80px))`.
- Mobile wrapper: `width: calc(100% - 40px)`.
- Every major lower section starts with a `1px solid var(--line)` rule.
- Use `box-sizing: border-box` globally.
- Hide horizontal overflow; collage objects may extend beyond their containing layer.

## Page structure

1. Full-screen hero / scrapbook cover.
2. Featured work with draggable paper cards.
3. Other work as a compact indexed list.
4. About copy and contact links.

Keep the page single-column in reading order even when the visual composition is layered.

## Hero / scrapbook cover

The hero is the visual signature of the project.

- Full viewport height: `height: 100svh`; minimum height around `680px` on desktop and `620–680px` at smaller sizes.
- Background: `#fffaf5` / `var(--paper)`.
- `position: relative`, `overflow: hidden`, `isolation: isolate`.
- Center copy is absolutely centered horizontally and placed around the upper-middle of the viewport.
- Hero copy width: `min(800px, 70vw)` on desktop; `92vw` on mobile.
- Hero name is centered and uses the handwritten font.
- Role text is around `17–22px`.
- Motto is italic and smaller, around `13–16px`.
- Supporting copy is around `16–21px`, with `1.3` line height and a maximum width around `700px`.
- Keep the center copy above collage layers with `z-index: 2`.

### Collage layers

- Left collage fills the hero height and is anchored to the left edge.
- Right still-life collage sits at the top-right, around `31vw` wide and no more than `90%` of the viewport height.
- Objects use `pointer-events: none` and should not interfere with navigation.
- Use transparent cut-outs and a large photographed base layer where possible.
- Object layering should feel physical: base paper first, then coffee/film/lighter, then foreground details.
- Use soft, low-opacity `drop-shadow` only when an object needs separation from the paper.
- Do not make decorative images compete with the center copy.

### Scroll cue

- Fixed near the bottom center of the hero, about `23px` from the bottom on desktop and `15px` on mobile.
- Typewriter glyphs, approximately `27px`, muted gray.
- The first glyph is partially transparent to create a repeated downward cue.

## Preloader

The preloader is a full-screen paper-colored transition, not a separate branded page.

- Fixed to all four edges with `z-index: 10000`.
- Background `#fffaf5`, text `#424044`.
- Thin inset frame: `24px` on desktop, `14px` on mobile.
- Large faint circular line decoration centered behind the copy.
- Content width: `min(760px, calc(100% - 48px))`.
- Label: `11px`, uppercase, `0.13em` tracking.
- Message: `clamp(22px, 4.6vw, 42px) / 1.3`.
- Status: `9px`, uppercase, muted; dots use the green accent.
- Encrypted characters use `#9caa87`; revealed characters use `#424044`.
- Sequence duration is about `2s`; hero copy reveals in small staggered steps.

## Section labels

Use a short descriptive label at the start of each major section:

```css
.section-label {
  margin: 0 0 25px;
  color: var(--ink);
  font: 20px/1.3 var(--typewriter);
  letter-spacing: -.025em;
}

.section-label span {
  margin-left: 5px;
  color: var(--warm-accent);
  font-size: .78em;
  vertical-align: middle;
}
```

The symbol after the label is optional but should be small and warm-colored.

## Featured project cards

Featured cards are tactile paper objects arranged as a loose stack.

- Stack width: `min(850px, 100%)`.
- Desktop stack height: approximately `430px`; tablet `370px`; mobile `min(88vw, 390px)`.
- Card width: `min(58%, 330px)` desktop; `min(68%, 300px)` mobile.
- Card height: `76–78%` of the stack.
- Card padding: `12px` desktop, `10px` mobile.
- Card border: `1px solid var(--line)`.
- Card radius: `19px`; artwork radius: `13px`.
- Card surface: `var(--paper-card)`.
- Shadow: `var(--float-shadow)`.
- Cards overlap and rotate slightly: approximately `-7deg`, `5deg`, and `-2deg`.
- Cards can be dragged with a pointer and nudged with arrow keys.
- Keep movement bounded by the stack frame.
- Show a small pill hint near the top-right: `9px` typewriter text, `8px 11px` padding, rounded border.

Card anatomy:

1. Artwork block: about `54%` of the card height.
2. Metadata row: `8px` typewriter text, muted.
3. Project name: `17px / 1.2`.
4. Description: `9px / 1.45`.
5. Bottom category row separated by a thin rule, with a warm arrow.

Artwork should use abstract organic shapes rather than generic icons. Shapes can be CSS-generated with large asymmetric border radii and muted peach, sage, or blue fills.

## Other work list

- Section has the same `var(--section-pad)` rhythm as Featured Work.
- List has a top border and a bottom border on every row.
- Desktop row minimum height: `94px`.
- Desktop columns: index, main content, type, year, arrow.
- Approximate desktop grid: `44px minmax(240px, 1fr) 160px 54px 20px`.
- Use flexible gaps: `clamp(12px, 2vw, 22px)`.
- Index/type/year use `11px / 1.4` muted mono text.
- Project title uses `17px / 1.25` typewriter text.
- Summary uses `12px / 1.45` muted text.
- On hover, add a subtle warm-tinted background and `10px` horizontal padding.
- Arrow is `17px` and warm-colored.

## About and contact

- Desktop layout: two columns, approximately `.82fr 1.18fr`.
- Column gap: `clamp(28px, 6vw, 76px)`.
- Body max width: `620px`.
- Lead paragraph: `20px / 1.55`, dark ink, bottom margin `24px`.
- Regular paragraphs: `14px / 1.8`, muted body ink, bottom margin `19px`.
- Signoff: handwritten font, `32px / 1.1`, warm accent, with roughly `26px 0 30px` margin.
- Contact block starts with a top rule and `20px` top padding.
- Contact text: `11px / 1.5` typewriter.
- Social links use a small gap (`18px`) and lift by about `2px` on hover.

## Responsive behavior

### Around `900px`

- Reduce hero collage width and move the right collage lower.
- Center hero copy in about `82vw`.
- Reduce supporting copy toward `14–17px`.
- Use tighter list columns and gaps.

### Around `850px`

- Section padding becomes `52px`.
- Other-work grid becomes less dense.
- About columns narrow toward `.75fr 1.25fr`.

### Around `700px`

- Wrapper becomes `calc(100% - 40px)`.
- Section padding becomes `42px`; bottom padding around `72–76px`.
- Project cards stay layered instead of becoming a normal grid.
- Other-work list hides type and year columns.
- Row grid becomes approximately `26px minmax(0, 1fr) 18px`.
- About section becomes one column.
- Contact links stack vertically.

### Around `600px`

- Hero keeps the center copy at about `31%` from the top.
- Hero name scales between `68px` and `86px`.
- Supporting copy becomes about `13px`, max width `330px`.
- Collage fills the viewport more aggressively but stays visually subordinate with reduced opacity.
- Preloader frame shrinks to `14px`; message becomes `clamp(20px, 6vw, 30px)`.

## Interaction and motion

- Smooth scrolling is enabled for normal users.
- Link hover: change to `var(--warm-accent)`; avoid large transforms.
- Contact links may translate upward about `2px`.
- Project cards use `grab` / `grabbing`, preserve touch interaction with `touch-action: none`, and remain keyboard-nudgeable.
- Hero content fades/slides upward about `14px` over `.5s`, with roughly `.08s` staggered delays.
- Preloader fades over roughly `2s`.
- Keep transitions short: `.2–.3s`, usually ease-in-out.

## Accessibility rules

- Preserve semantic headings, sections, navigation, articles, and links.
- Every decorative image has an empty `alt` and `aria-hidden="true"`.
- Decorative collage layers must not receive focus.
- Keep a visible focus outline: `2px solid var(--warm-accent)` with `4px` offset.
- Draggable cards must also work with arrow keys and have an accessible label explaining the interaction.
- Respect `prefers-reduced-motion: reduce`: disable smooth scrolling, animations, and transitions; show the portfolio immediately and reveal text without scrambling.
- Do not communicate important information through color alone.
- Maintain readable contrast for body text and focus indicators against the paper background.

## Content voice

- Personal, thoughtful, direct, and a little playful.
- Short labels are better than marketing-heavy headings.
- Explain what was made in plain language.
- Keep project metadata compact: type/category plus year.
- Use sentence case for content; reserve uppercase for small technical metadata.

## Current content model

The existing project uses:

- Identity: `Abhiraj`.
- Role: `Software Developer & Network Engineer`.
- Motto: `Verb & Noun`.
- Hero description: thoughtful process, clarity, and delight.
- Featured work: three draggable cards, each with a name, detail, category/year, artwork color, and external URL.
- Other work: indexed rows with name, type, year, summary, and external URL.
- About: a short first-person story followed by LinkedIn, Instagram, GitHub, and email links.

For a new project, keep this content structure but replace the words, links, and artwork—not the layout rules.

## Implementation notes

- The implementation uses React, Vite, and plain CSS; no component library is required.
- Keep design tokens in one `:root` block so a new project can retheme the system quickly.
- Reuse native CSS layout, pointer events, transitions, and media queries before adding dependencies.
- Keep image assets in a replaceable folder and reference them as layers.
- The final declarations in the stylesheet define the current effective design language; older declarations document the earlier editorial direction and may be removed during a cleanup.

## Do not add by default

- Bright gradients, heavy glassmorphism, neon colors, or dense card dashboards.
- Large drop shadows, excessive rounded containers, or decorative UI without a purpose.
- New font families for isolated elements.
- Motion that blocks reading or interaction.
- A new component/animation dependency for effects achievable with CSS and native pointer events.
