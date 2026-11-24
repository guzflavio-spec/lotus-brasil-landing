# Creative Agency Agent

A Claude Code subagent that works as a full creative agency: strategy, concept,
copy, art direction, video production prompts and a production plan with costs.

## Use

In Claude Code, from this repo:

```
Use the creative-agency agent to build a 15 s Reels campaign for <brief>
```

The agent definition is `.claude/agents/creative-agency.md`.

## Layout

```
.claude/agents/creative-agency.md   the agent (roles, pipeline, rules)
creative-agency/
  prompts/PLAYBOOK.md               prompt formulas and workflow
  prompts/templates/                ready-to-adapt templates
  prompts/sources/                  community libraries (CC BY 4.0)
  prompts/ATTRIBUTION.md            credits and licences
  projects/                         deliverables (created per brief)
```

## Notes

- Prompt sources keep their original licences. See `prompts/ATTRIBUTION.md`.
- Spending generation credits (ElevenLabs, Veo, Kling...) always needs your OK first.
- To use it as a standalone repository, copy `.claude/agents/` and `creative-agency/`
  to a new repo.
