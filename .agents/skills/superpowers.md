# Skill: superpowers

## Purpose
Lock down a concrete implementation plan and verification criteria for multi-file features, complex logic, or architecture changes — before writing a single line of application code.

## When to Activate
- Any task touching more than two files
- New feature requiring a migration, model, controller, and view
- Refactor that changes public interfaces or shared contracts
- Any task where edge cases or rollback matter

## Procedure
1. **Restate the goal** – one sentence, in terms of user-visible outcome.
2. **List files to change** – explicit paths, no wildcards.
3. **Outline steps** – ordered, atomic, reversible where possible.
4. **Call out edge cases** – empty states, auth boundaries, concurrent writes, mobile viewports.
5. **Define verification** – the exact checks (manual steps, `php artisan test`, visual states) that prove the task is complete.
6. **Identify rollback** – what to undo if something goes wrong.

## Output Contract
```
Goal: <sentence>
Files:
  - path/to/file.php  (reason)
Steps:
  1. …
  2. …
Edge cases:
  - …
Verification:
  - …
Rollback:
  - …
```

## Constraints
- No code written during this phase.
- Plan must be approved (or self-validated against the task spec) before handing off to `ponytail`.

