# Agent instructions

## Agent skills

If a prompt starts with `/<name>` and that skill isn't loaded, read its `SKILL.md` from the table and follow it.

User-only skills have `disable-model-invocation: true` and must be explicitly requested by the user.

| Skill | SKILL.md path | User-only |
| --- | --- | --- |
| ask-matt | `.agents/skills/ask-matt/SKILL.md` | Yes |
| grilling | `.agents/skills/grilling/SKILL.md` | No |
| grill-with-docs | `.agents/skills/grill-with-docs/SKILL.md` | Yes |
| domain-modeling | `.agents/skills/domain-modeling/SKILL.md` | No |
| prototype | `.agents/skills/prototype/SKILL.md` | No |
| handoff | `.agents/skills/handoff/SKILL.md` | Yes |
| to-spec | `.agents/skills/to-spec/SKILL.md` | Yes |
| to-tickets | `.agents/skills/to-tickets/SKILL.md` | Yes |
| implement | `.agents/skills/implement/SKILL.md` | Yes |
| tdd | `.agents/skills/tdd/SKILL.md` | No |
| code-review | `.agents/skills/code-review/SKILL.md` | No |
| codebase-design | `.agents/skills/codebase-design/SKILL.md` | No |
| pr | `.agents/skills/pr/SKILL.md` | No |
| retro | `.agents/skills/retro/SKILL.md` | Yes |
| writing-for-agents | `.agents/skills/writing-for-agents/SKILL.md` | No |
| diagnosing-bugs | `.agents/skills/diagnosing-bugs/SKILL.md` | No |
| research | `.agents/skills/research/SKILL.md` | No |
| wayfinder | `.agents/skills/wayfinder/SKILL.md` | Yes |
| setup-matt-pocock-skills | `.agents/skills/setup-matt-pocock-skills/SKILL.md` | Yes |
| karpathy-guidelines | `.agents/skills/karpathy-guidelines/SKILL.md` | No |
| impeccable | `.github/skills/impeccable/SKILL.md` | No |
| accessibility | `.agents/skills/accessibility/SKILL.md` | No |
