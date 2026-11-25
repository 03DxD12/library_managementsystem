# Skill: emil-design-eng

## Purpose
Tune all interactive transitions and micro-interactions: modals, drawers, tooltips, toasts, loading states, and any other motion that provides feedback.

## When to Activate
- Adding or modifying: modals, off-canvas drawers, tooltips, popovers, toasts, collapse panels
- Any element that enters, exits, or changes state visually
- Adding loading spinners, skeleton screens, or progress indicators

## Animation Rules (strict)
| Rule | Detail |
|------|--------|
| Duration | Entrances ≤ 250ms · Exits ≤ 200ms · Never exceed 300ms |
| Properties | Only `transform` and `opacity` (GPU-composited). Never animate `height`, `width`, `top`, `margin`, `padding`, or `color`. |
| Easing | Entrances: `cubic-bezier(0.22, 1, 0.36, 1)` (ease-out). Exits: `cubic-bezier(0.4, 0, 1, 1)` (ease-in). Never use bare `ease-in` on entrances. |
| Scale | Never scale from `0`. Minimum entrance scale: `0.95`. |
| High-frequency | Never animate elements triggered more than once per second (e.g., scroll events, live counters). |
| `prefers-reduced-motion` | Wrap all custom animations in `@media (prefers-reduced-motion: no-preference)`. Provide an instant fallback. |

## Procedure
1. List every interactive element added or changed.
2. For each: define enter state → active state → exit state.
3. Write CSS transitions using only the approved properties and easings.
4. Add `@media (prefers-reduced-motion: no-preference)` wrappers.
5. Test by triggering each interaction at least three times and confirming it feels snappy, not floaty.

## Output
Annotated list of elements with their transition definitions.

## Constraints
- Never use `transition: all`.
- Never use JS `setTimeout` to fake animation timing — use `transitionend` events.
- Bootstrap's built-in transitions are acceptable; override only when they violate the rules above.

