# Skill: frontend-design

## Purpose
Define clean visual hierarchy, intentional typography, and a restrained colour palette for new pages or views — before markup is written.

## When to Activate
- Designing a new Blade view or page from scratch
- Introducing a new section with its own layout grid
- Establishing visual language for a new feature area

## Skip When
- Only editing backend logic
- Polishing or tweaking existing UI (use `make-interfaces-feel-better` instead)
- Adding a small component to an already-designed page

## Procedure
1. **Identify the user's goal on this screen** – one job the page must accomplish.
2. **Define the layout grid** – columns, gutters, breakpoints. Use Bootstrap 5 grid tokens already in the project.
3. **Establish type scale** – map headings (h1–h4) and body sizes to existing CSS custom properties; do not introduce new font sizes.
4. **Colour palette** – use only existing CSS variables (`--bs-*` or project tokens); flag if a new colour is truly needed.
5. **Component inventory** – list Bootstrap 5 components to reuse (cards, tables, badges, modals) so nothing is built from scratch.
6. **Sketch the hierarchy** – describe the visual weight order (primary CTA, secondary info, tertiary metadata).

## Output Contract
```
Page goal: <sentence>
Grid: <columns/breakpoints>
Type scale: <tokens used>
Colours: <tokens used>
Components: [list]
Hierarchy:
  1. <most prominent>
  2. …
```

## Constraints
- No markup written during this phase.
- Never introduce a new typeface or colour without explicit approval.

