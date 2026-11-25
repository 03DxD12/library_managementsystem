# Skill: make-interfaces-feel-better

## Purpose
A targeted CSS/styling pass that applies optical polish: concentric radii, proper alignment, legible typography, and correct hit-target sizing.

## When to Activate
- Any CSS or Blade styling pass on existing UI
- After `ponytail` build phase, before the accessibility audit
- When a UI feels "off" but functions correctly

## Checklist (apply every time)

### Border Radius — Concentric Rule
- Outer radius = inner element radius + padding gap.
- Example: card with `border-radius: 12px` and `8px` inner padding → child rounded element gets `border-radius: 4px`.
- Never apply the same radius to a parent and its direct child.

### Icon Centering — Optical Alignment
- Icons in buttons/badges must be visually centered, not mathematically centered.
- Use `display: flex; align-items: center; justify-content: center;` on the wrapper.
- For SVG icons, verify `viewBox` is not adding invisible padding.

### Numbers — Tabular Figures
- Any number that changes at runtime (counts, prices, stats, pagination): add `font-variant-numeric: tabular-nums;`.

### Headings — Balanced Wrapping
- Apply `text-wrap: balance;` to all `<h1>`–`<h4>` elements and card titles.

### Hit Targets — Minimum Size
- Every clickable or tappable element must be at least `40×40px` (use padding, not `min-height` alone).
- Check buttons, icon-only links, close buttons, and table row actions.

### Transitions — No `all`
- Find and replace every `transition: all` with explicit property lists.
- Acceptable: `transition: opacity 150ms ease-out, transform 150ms ease-out;`

### Spacing — 4px Grid
- All margins, paddings, and gaps must be multiples of `4px`. Flag any odd values.

## Output
Bullet list of changes with `file:line` references.

## Constraints
- Do not change colours, fonts, or layout during this pass — only the properties above.
- Do not add new CSS classes; extend existing ones or add targeted overrides.

