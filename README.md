# skill-author

Write Claude Code skills that Claude picks up and follows. `skill-author` walks you through making one: what it covers, when it should fire, what belongs in `SKILL.md` and what moves out to companion files, and whether it needs a script.

It ships with `writing-great-skills`, a reference on what makes a skill behave the same way every run. `skill-author` loads it before drafting anything.

It's a Claude Code plugin from Family IT Guy. Both skills are adapted from [Matt Pocock's skills](https://github.com/mattpocock/skills).

## What it does

- It asks before it drafts: what the skill covers, the cases it has to handle, whether it needs scripts, and what reference material to include.
- It writes the description for the moment the skill should fire. The description is the only part of a skill Claude sees when deciding what to load, so it says what the skill does and when to use it. It never summarizes the steps, because Claude would follow the summary and never open the skill.
- It keeps `SKILL.md` short. Detail that only some uses need goes into a companion file behind a pointer.
- It runs the skill once on a real case. Before you rely on a new or edited skill, it has an agent use it on one real task and compares what the agent did with what the skill says. Where they differ, the skill changes. Edits get tested in a fresh session, because a skill edited mid-session doesn't reach the session that edited it.

## When to reach for it

- You're writing a new skill.
- A skill you have gets ignored, fires at the wrong time, or gets followed only partly, or it has grown long and needs splitting.

## Install

```
/plugin marketplace add Family-IT-Guy/plugins
/plugin install skill-author@familyitguy
```

Restart Claude Code, then ask for help building a skill, or type `/skill-author:skill-author`.

To update later: `/plugin marketplace update familyitguy` then `/plugin install skill-author@familyitguy`. (Or turn on auto-update in the `/plugin` menu under Marketplaces.)
