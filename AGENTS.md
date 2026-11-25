# AGENTS.md — Library Content Management System

This file configures automatic skill routing for Antigravity and Codex agents working
in this repository. Skills live in `.agents/skills/`. Read and apply the matching skill
at the phase described below — do not apply multiple skills simultaneously to avoid
conflicts.

---

## Skill Routing Rules

| Skill | File | Activate When |
|---|---|---|
| `understand-anything` | `.agents/skills/understand-anything.md` | Mapping unfamiliar modules OR analyzing diff impact on shared core files |
| `superpowers` | `.agents/skills/superpowers.md` | Multi-file features, complex logic, or architecture changes — plan before coding |
| `frontend-design` | `.agents/skills/frontend-design.md` | Designing new pages, views, or visual layouts from scratch |
| `ponytail` | `.agents/skills/ponytail.md` | **ALL** coding tasks (full mode) — enforce minimal diffs, native APIs, reuse existing helpers |
| `emil-design-eng` | `.agents/skills/emil-design-eng.md` | Adding or modifying transitions, modals, drawers, tooltips, or interactive feedback |
| `make-interfaces-feel-better` | `.agents/skills/make-interfaces-feel-better.md` | CSS/styling passes — concentric radii, optical alignment, hit targets, typography |
| `web-design-guidelines` | `.agents/skills/web-design-guidelines.md` | **Final step** on every UI task — audit accessibility, focus states, semantic HTML |

---

## Standard Agent Pipeline

When executing any UI/frontend task, run phases in this strict order:

```
1. understand-anything  →  Map dependencies, shared surfaces, risk zones
2. superpowers          →  Lock down plan + verification criteria
3. frontend-design      →  Visual hierarchy (SKIP for backend-only or polish tasks)
4. ponytail (full)      →  Surgical implementation with minimal diffs
5. emil-design-eng      →  Tune transitions and micro-interactions
6. make-interfaces-feel-better → CSS polish pass
7. web-design-guidelines → Accessibility + semantic audit (fix before marking done)
```

**Do not skip phases** unless the skip condition is explicitly stated in the skill file.
**Do not run overlapping skills simultaneously** — complete each phase fully before starting the next.

---

## Project Context

| Property | Value |
|---|---|
| Framework | Laravel 11 (PHP 8.2+) |
| Frontend | Blade + Bootstrap 5 + Vite |
| CSS tokens | Bootstrap 5 `--bs-*` custom properties |
| Design grid | Bootstrap 5 12-column, 4px base unit |
| Animation budget | Entrance ≤ 250ms · Exit ≤ 200ms · Max 300ms |
| Min hit target | 40 × 40 px |
| Contrast standard | WCAG 2.1 AA (4.5:1 body, 3:1 large/UI) |

---

## Scope Boundaries

- `understand-anything` → **read-only**; never modify application code during this phase.
- `superpowers` → **plan-only**; no code written until plan is validated.
- `frontend-design` → **spec-only**; no markup written during this phase.
- `ponytail` → no new Composer/NPM packages without explicit user approval.
- `web-design-guidelines` → never mark a task complete with known open accessibility issues.

---

## Part 2 Task Placeholder

> **For the agent:** When a user provides a concrete task, replace the placeholder below
> and execute the full pipeline above, reporting briefly after each phase with a
> `file:line` summary of changes made.

```
Current task: [NO ACTIVE TASK — await user instruction]
```

---

*Last updated: 2026-11-26 by @03DxD12 (Denmhar Dimaculangan)*

