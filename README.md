# skill-author

Write skills your AI picks up and follows. `skill-author` walks you through making one: what it covers, when it should fire, what belongs in `SKILL.md` and what moves out to companion files, and whether it needs a script.

It ships with `writing-great-skills`, a reference on what makes a skill behave the same way every run. `skill-author` loads it before drafting anything.

They're skills from Family IT Guy, and they work with any AI model and any tool that uses skills. Both are adapted from [Matt Pocock's skills](https://github.com/mattpocock/skills).

## What it does

- It looks before it asks. It reads your existing skills and past work for what it needs, and asks you only for what it can't find.
- It checks whether a skill you already have fires at the same moment. If one does, it suggests changing that skill instead of adding a second.
- It writes the description for the moment the skill should fire. The description is the only part of a skill the AI sees when deciding what to load, so it says what the skill does and when to use it. It never summarizes the steps, because the AI would follow the summary and never open the skill.
- It keeps `SKILL.md` short. Detail that only some uses need goes into a companion file behind a pointer, and it cuts any sentence that changes nothing.
- It shows you the full draft and where it will be saved, and saves nothing until you approve.
- It runs the skill once on a real case. Before you rely on a new or edited skill, it has an agent use it on one real task and compares what the agent did with what the skill says. Where they differ, the skill changes. Edits get tested in a fresh session, because a skill edited mid-session doesn't reach the session that edited it.

## When to reach for it

- You're writing a new skill.
- A skill you have gets ignored, fires at the wrong time, or gets followed only partly, or it has grown long and needs splitting.

## Install

The skills are the folders `skills/skill-author` and `skills/writing-great-skills`.

- If your tool loads skills, put both folders where it looks for them.
- If it doesn't, give your AI the files in both folders and ask it to follow `skill-author` when you want a skill built or fixed.
- The setup prompt in [ai-instruction-router](https://github.com/Family-IT-Guy/ai-instruction-router) can install them for you in whatever tool you use.

In Claude Code you can install them from the Family IT Guy plugin marketplace instead:

```
/plugin marketplace add Family-IT-Guy/plugins
/plugin install skill-author@familyitguy
```

Then ask for help building a skill. To update later: `/plugin marketplace update familyitguy` then `/plugin install skill-author@familyitguy`.
