---
name: Sop
description: Write, audit, and improve Standard Operating Procedures (SOPs) that reliably guide both human and AI agents. Applies the 7-layer prompt architecture — procedures over abstractions, motivation with directives, measurable constraints, anti-rationalization rules, first-class verification, layered trust, and constraint repetition. USE WHEN create an SOP, write an SOP, draft a procedure, audit SOPs, review SOPs, improve SOPs, or ask for an SOP template.
---

# SOP Authoring Skill

> Create, audit, and improve Standard Operating Procedures (SOPs) that reliably guide both human and AI agents.

## When This Skill Activates

- User asks to "create an SOP", "write an SOP", "draft a procedure"
- User asks to "audit SOPs", "review SOPs", "improve SOPs"
- User asks for an "SOP template"

---

## Core Principles

These principles are derived from the 7-layer prompt architecture and operational experience across the metafactory ecosystem.

### 1. Procedures Over Abstractions

Never write "be careful" or "handle appropriately." Instead, describe the exact steps with explicit success criteria.

**Bad:** "Ensure code quality before merging."
**Good:** "1. Run `bun test` — all tests must pass. 2. Run `bun run typecheck` — zero errors. 3. Run `bun run lint` — zero warnings. 4. Get at least one reviewer approval. 5. Verify CI pipeline is green."

Every instruction must be verifiable by a third party who wasn't present when it was written.

### 2. Add Motivation, Not Just Directives

Rules with reasons generalize better than bare rules. Include the "why" so agents can make correct decisions in edge cases.

**Bad:** "Do not summarize the diff at the end."
**Good:** "Do not summarize the diff at the end. The user can inspect the diff directly, so summaries add noise. Only summarize when it helps the user decide what to do next."

### 3. Measurable Constraints Over Vague Words

Replace subjective terms with testable criteria.

| Vague | Measurable |
|-------|-----------|
| "Be concise" | "Response must be under 200 words" |
| "Be thorough" | "Cover all files matching `src/**/*.ts`" |
| "Handle errors properly" | "Every catch block must log, handle, or explicitly ignore with comment" |
| "Keep it clean" | "Zero lint warnings, no unused imports" |

### 4. Anti-Rationalization Rules

Explicitly name the shortcuts agents are likely to take and block them. This is the most underused and most powerful pattern.

Include a section in every SOP:

```
## What NOT To Do
- Do not claim success without running the verification checklist
- Do not skip steps because they "probably" aren't needed
- Do not assert file contents without reading them
- Do not treat a passing unit test as proof the full workflow works
- Do not ask broad clarifying questions when one specific question suffices
```

### 5. Verification as a First-Class Citizen

Every SOP must end with a verification checklist. The checklist must be:
- **Independently executable** — someone who didn't write the SOP can run it
- **Binary** — each item is pass/fail, not subjective
- **Complete** — covers all outputs the SOP claims to produce

### 6. Layered Trust Architecture

SOPs should specify which inputs are trusted and which are not:
- **Policy** (the SOP itself) = highest trust
- **Runtime context** (env vars, config) = trusted
- **Retrieved context** (search results, API responses) = verify before acting
- **User input** = validate at boundaries

### 7. Constraint Repetition at Failure Points

Critical rules should appear both globally AND at each step where they might be violated. This is not redundancy — it is fault containment.

Example: If "never push to main without PR" is critical, it should appear in:
- The global rules section
- The "publish" step specifically
- The verification checklist

---

## SOP Creation Workflow

When asked to create a new SOP, follow this procedure:

### Phase 1: Scope

1. **Identify the trigger** — What event or request activates this SOP?
2. **Identify the audience** — Who will follow it? (humans, agents, or both)
3. **Identify existing SOPs** — Search `docs/sops/` to avoid duplication
4. **Identify the source of truth** — What research, design decisions, or incidents inform this SOP?

### Phase 2: Draft

5. **Write the header** — Purpose, status, derived-from, audience
6. **Write the trigger conditions** — Specific, testable conditions for when to run this SOP
7. **Write prerequisites** — Checklist of what must be true before starting
8. **Write steps** — Numbered, imperative, each with:
   - The action (what to do)
   - The motivation (why)
   - The success criterion (how to verify)
   - The anti-pattern (what NOT to do)
9. **Write the verification checklist** — Binary pass/fail items covering all outputs
10. **Write the "What NOT To Do" section** — Anti-rationalization rules specific to this SOP

### Phase 3: Validate

11. **Walk-through test** — Mentally execute the SOP against a real scenario. Does every step produce a clear, verifiable output?
12. **Edge case check** — What happens if a step fails? Is the recovery path documented?
13. **Duplication check** — Does this overlap with existing SOPs? If so, reference rather than duplicate.
14. **Measurability check** — Replace every vague term found during walk-through with a testable constraint.

### Phase 4: Publish

15. **Number the SOP** — Next sequential number in the series (SOP-10, SOP-11, ...)
16. **Add to index** — Update `docs/sops/README.md` with the new entry
17. **Commit with reference** — `docs: add SOP-{N} — {title}`
18. **Announce** — Post to the relevant channel

---

## SOP Audit Workflow

When asked to audit existing SOPs:

1. **Read all SOPs** in `docs/sops/` — every file, not just the one mentioned
2. **Score each SOP** against the 7 principles above (0-2 per principle, max 14)
3. **Identify gaps** — Which principles are violated? Be specific: quote the line.
4. **Propose fixes** — For each gap, write the improved text
5. **Prioritize** — Order fixes by impact (anti-rationalization rules and verification checklists are highest priority)

### Audit Scoring Guide

| Score | Meaning |
|-------|---------|
| 0 | Principle not addressed at all |
| 1 | Principle partially addressed (some steps vague, some measurable) |
| 2 | Principle fully addressed (all steps specific, verifiable, motivated) |

---

## SOP Template

When asked for a template, provide this:

````markdown
# SOP-{N}: {Title}

**Purpose:** {One sentence — what problem this SOP solves}
**Status:** Draft
**Derived from:** {Research doc, DD number, incident, or experience}
**Audience:** {Humans, agents, or both}

---

## When to Trigger

Run this SOP when:
- {Specific condition 1}
- {Specific condition 2}

## Prerequisites

- [ ] {Prerequisite 1}
- [ ] {Prerequisite 2}

---

## Steps

### 1. {Step Title}

**Action:** {What to do — imperative, specific}
**Why:** {Motivation — why this step matters}
**Verify:** {How to confirm this step succeeded — binary test}
**Anti-pattern:** {What NOT to do at this step}

### 2. {Step Title}

...

---

## What NOT To Do

- Do not {common shortcut 1} — because {consequence}
- Do not {common shortcut 2} — because {consequence}

---

## Verification Checklist

After completing all steps, verify:

- [ ] {Output 1 exists and is correct}
- [ ] {Output 2 meets criteria}
- [ ] {No side effects — nothing broken}

---

*This SOP is a living document. Update it as the process evolves.*
````

---

## Quality Bar

An SOP produced by this skill must score at least 10/14 on the audit scoring guide before being considered complete. If it scores below 10, iterate until it does.
