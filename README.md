# metafactory-skill-sop

SOP authoring skill for metafactory agents. Teaches agents how to write, audit, and improve Standard Operating Procedures using principles from the [Claude Code prompt playbook](https://github.com/kropdx/unofficial-claude-code-prompt-playbook).

## Install

```bash
arc install the-metafactory/metafactory-skill-sop
```

## What It Does

- **Create SOPs** — Guides agents through a 4-phase workflow (Scope → Draft → Validate → Publish) producing SOPs that are specific, verifiable, and motivated
- **Audit SOPs** — Scores existing SOPs against 7 quality principles and proposes targeted fixes
- **SOP Template** — Provides a battle-tested template with anti-rationalization rules and verification checklists

## Principles

Derived from the 7-layer prompt architecture:

1. **Procedures over abstractions** — Exact steps, not vague guidance
2. **Motivation with directives** — Rules with reasons generalize better
3. **Measurable constraints** — Testable criteria, not subjective terms
4. **Anti-rationalization rules** — Block common agent shortcuts explicitly
5. **Verification as first-class** — Every SOP ends with binary pass/fail checklist
6. **Layered trust** — Specify what's trusted vs what needs verification
7. **Constraint repetition** — Critical rules appear at every failure point

## For Network Operators

This skill is designed for metafactory network operators who want their agents to produce consistent, high-quality operational procedures. Install it network-wide to establish a shared quality bar for all SOPs.

## License

MIT
