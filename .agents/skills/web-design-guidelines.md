# Skill: web-design-guidelines

## Purpose
Final compliance audit on all touched frontend files: keyboard navigation, visible focus rings, semantic HTML, WCAG 2.1 AA, and ARIA standards.

## When to Activate
- Before finishing ANY UI task that modifies Blade templates, CSS, or JS
- As the last phase of the agent skill pipeline

## Audit Checklist

### 1. Semantic HTML
- [ ] Headings follow a logical hierarchy (no skipped levels: h1 → h2 → h3).
- [ ] Interactive elements use `<button>` (not `<div>` or `<span>` with click handlers).
- [ ] Forms use `<label for="id">` paired with `<input id="id">` — no placeholder-only labels.
- [ ] Lists of items use `<ul>`/`<ol>`; navigation uses `<nav>`.
- [ ] Data tables use `<th scope="col/row">` and a `<caption>`.

### 2. Keyboard Navigation
- [ ] All interactive elements are reachable via `Tab` in a logical order.
- [ ] `tabindex` values are only `0` or `-1` — never positive integers.
- [ ] Modals trap focus while open and restore focus to the trigger on close.
- [ ] Dropdowns and custom menus respond to `Escape` to close.

### 3. Focus Rings
- [ ] No `outline: none` or `outline: 0` without a custom `:focus-visible` replacement.
- [ ] Focus ring is visible against both light and dark backgrounds (min 3:1 contrast).

### 4. Colour & Contrast (WCAG 2.1 AA)
- [ ] Text contrast ratio ≥ 4.5:1 for body text.
- [ ] Large text (≥ 18pt / 14pt bold) contrast ratio ≥ 3:1.
- [ ] Interactive component boundaries (buttons, inputs) ≥ 3:1 against background.
- [ ] No information conveyed by colour alone.

### 5. ARIA
- [ ] `aria-label` or `aria-labelledby` on icon-only buttons.
- [ ] `role="alert"` or `aria-live="polite"` on dynamic status messages/toasts.
- [ ] `aria-expanded` on toggle buttons (menus, accordions).
- [ ] `aria-hidden="true"` on decorative icons/SVGs.
- [ ] No redundant ARIA roles on native elements (e.g., `role="button"` on `<button>`).

### 6. Images & Media
- [ ] Every `<img>` has a meaningful `alt` attribute (or `alt=""` if decorative).
- [ ] No text embedded in images without a text equivalent.

### 7. Reduced Motion
- [ ] All custom CSS animations are inside `@media (prefers-reduced-motion: no-preference)`.

## Procedure
1. Open each modified Blade/HTML/CSS file.
2. Work through the checklist top-to-bottom.
3. For each failure: fix inline and note `file:line — issue — fix`.
4. Re-read the diff to confirm no accessibility regression was introduced by the fix itself.

## Output
```
Audit result: PASS / FAIL (n issues fixed)
Fixes:
  - file:line — issue — fix applied
```

## Constraints
- Never mark an audit as PASS with known open issues.
- Fixes must not change visual design — only accessibility attributes, semantic elements, and focus styles.

