# Domain docs

This repository uses a single context: `GLOSSARY.md` at the repository root and architecture decision records under `docs/adr/`.

## Before exploring

Read `GLOSSARY.md` and any ADRs relevant to the area being explored.

If these documents do not exist, continue without flagging their absence or proposing scaffolding. The `domain-modeling` skill creates them lazily when terminology or decisions are resolved.

## File structure

```text
GLOSSARY.md
docs/
  adr/
    0001-decision-title.md
```

## Use the glossary's vocabulary

Use the glossary's terms when naming domain concepts in issues, proposals, hypotheses, and tests. When a needed concept is missing, reconsider whether it belongs to the domain or note the gap for `domain-modeling`.

## Flag ADR conflicts

If a proposal contradicts an existing ADR, identify the ADR and explain why the decision should be reopened rather than silently overriding it.
