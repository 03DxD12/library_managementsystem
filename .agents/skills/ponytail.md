# Skill: ponytail (Full Mode)

## Purpose
Implement changes with surgical, minimal diffs. Reuse every existing helper, utility, and native browser API. No bloat, no new dependencies, no unnecessary abstractions.

## When to Activate
- ALL coding tasks — this skill is always active during the Build phase.

## Core Rules (non-negotiable)
1. **Minimal diff** – change only lines directly required by the task. Leave surrounding code untouched.
2. **Reuse first** – before writing a helper, search the codebase. Use existing traits, scopes, components, and Blade partials.
3. **Native over library** – prefer PHP built-ins, Laravel core APIs, and vanilla JS over adding a package.
4. **No dead code** – do not leave commented-out code, unused imports, or stale variables.
5. **Preserve contracts** – keep method signatures, validation rules, CSRF tokens, and error handling intact.
6. **One responsibility per commit** – each logical change is a discrete, reviewable unit.
7. **No `dd()`, `var_dump()`, or debug output** in committed code.

## Procedure
1. Apply the plan from `superpowers`.
2. For each file: open → locate the exact insertion/change point → make the smallest valid edit.
3. After each file edit, re-read the diff mentally and ask: "Is every changed line necessary?"
4. Run `php artisan test` (or the relevant subset) after all edits.
5. Fix failures before moving to the next phase.

## Constraints
- Never rewrite a file wholesale when a targeted edit suffices.
- Never install a Composer or NPM package without explicit approval.
- Never bypass middleware, policies, or form request validation.

