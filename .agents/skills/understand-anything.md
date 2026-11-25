# Skill: understand-anything

## Purpose
Map unfamiliar modules and analyze the impact of diffs on shared core files before any coding begins.

## When to Activate
- Opening a file or module you have never edited before
- Tracing a cross-cutting change that touches shared utilities, middleware, or base classes
- Assessing blast radius of a planned refactor across multiple consumers

## Procedure
1. **Locate entry points** – find the route, controller, or service that owns the feature.
2. **Trace the dependency graph** – follow imports, service-container bindings, and event listeners one level deep.
3. **Identify shared surfaces** – note any helpers, traits, or base classes used by more than one consumer.
4. **Flag risk zones** – list files where a change could have unintended side-effects.
5. **Summarise in one paragraph** – state what the module does, what it depends on, and what depends on it.

## Output Contract
Return a brief map:
```
Module: <name>
Entry: <file:line>
Depends on: [list]
Used by: [list]
Risk zones: [list]
Summary: <one paragraph>
```

## Constraints
- Read-only phase — do not modify application code during this skill.
- Stop after the summary; pass findings directly to `superpowers` for planning.

