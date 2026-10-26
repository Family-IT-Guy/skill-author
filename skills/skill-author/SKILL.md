---
name: skill-author
description: Creates, rewrites, splits or reviews agent skills with the right structure, progressive disclosure and bundled resources. Use when the user wants to create, write, build or edit a skill, turn a repeated task, a correction or an outside skill into one, or when a skill gets ignored, fires at the wrong time, is followed only partly, or has grown too long.
---

# Writing Skills

A skill makes an agent take the same process every run. **Predictability** is the test for every line below. Context is finite, so a skill loads in layers: the description is always in context and decides when the skill fires, the body loads only when it fires, and sibling files load only for the branches that need them. Each layer holds only what its moment needs.

Before drafting or editing a skill, load the `writing-great-skills` skill for the vocabulary used below; if this harness can't load it by name, read its `SKILL.md` and `GLOSSARY.md` directly. Installed as a plugin, its name may carry a prefix, such as `skill-author:writing-great-skills`. `GLOSSARY.md` holds the full definitions. If a `personal.md` sits beside this file, read it too: it holds the owner's own values.

## Steps

1. **Gather.** Get the task the skill covers, its distinct **branches** (the different cases it must handle), whether any part is deterministic enough for a script, and what reference material exists. Inspect what you can yourself (past conversations, the existing skills and rules) and ask the user only for what you cannot find, because their attention costs more than your search. Done when you can name every branch in one line each.

2. **Check for overlap.** List the installed skills whose descriptions would fire on the same moment. If one already covers this, propose an edit to it rather than a new skill, because two skills for one moment compete and neither fires reliably. If the overlap is partial, write the boundary into both descriptions. Done when every competing description has been read and its boundary written down.

3. **Write the description.** It is the only text an agent sees when deciding whether to load the skill, and it sits in context every turn.
   - First sentence: what the skill does, in the third person. Second: "Use when" followed by concrete moments — words the user says, a point in a task, a file type, a claim about to be made. "When relevant" is not a moment.
   - One trigger per branch. Synonyms for one branch are duplication.
   - Never summarize the steps, because an agent that reads a summary follows it and never opens the body.
   - Put the key use case first and keep it short: harnesses cut long descriptions in the list the agent chooses from, so find the user's harness's limit in its current documentation.
   - Leave out owner names, accounts and repos, because skills get shared and specifics go stale.

   Done when every branch from step 1 has exactly one trigger and nothing in the description summarizes the steps.

4. **Draft the body**, aiming for under 100 lines.
   - Steps first. End each one with a checkable **completion criterion** ("every X accounted for", not "review X"), because a vague finish line gets skipped under the pull of the next step.
   - Put reference every branch needs inline. Move reference only some branches need into a sibling file (`REFERENCE.md`, or one named for what it holds) behind a pointer that says when to open it. Keep pointers one level deep.
   - Keep owner-specific values (paths, addresses, names, account or folder IDs) out of the body, in a sibling `personal.md` the body says to read when present, so the body stays one copy that can be shared and updated as is.
   - Say why in one sentence where a step could be misread. The reason is what lets the agent handle cases the skill never lists.
   - Use a pretrained **leading word** in place of a restated list.
   - Add a script in `scripts/` only when the operation is deterministic, the same code would otherwise be regenerated every run, or errors need explicit handling.
   - A skill only the user should start gets the harness's setting, where it has one, that keeps the agent from loading it on its own. Check what else that setting does in the user's harness: in some, the skill then carries no description in context and no other skill can load it.

   Done when every step ends with a completion criterion and the body is under 100 lines.

5. **Prune.** Every sentence costs context each time the skill loads. Test each one on its own and delete it whole if it is a **no-op** (the agent would do this anyway), **duplication** (another line or skill already says it), irrelevant (stale, or does not bear on the task) or **sediment** (an old patch a clear reason now covers). Done when every remaining sentence changes behavior.

6. **Present the draft for approval.** Show the full SKILL.md, any sibling files, the overlaps you found, and where it will be saved: the folder the user's harness loads skills from, for every project or for one project, or a plugin. Save nothing until the user approves, because a saved skill goes live in every session that loads that folder. Done when the user has approved the exact draft shown, or asked for changes.

7. **Run it once on a real case.** A draft is a hypothesis about what an agent will do, and reading it cannot test that. Put the skill in front of an agent **the way it will actually be reached** — by its description if it is model-invoked, or by name or path if only the user starts it — then give one real case, not a hypothetical, and compare what the agent does with what the skill says. Where they differ, the skill is the thing that changes. This applies to edits as well as new skills, which is where it is most often skipped.

   **A skill edited mid-session does not reach the agent that edited it.** Measured once: a step was added, then revised, then the skill was invoked, and the harness served the revision before it, matching neither the disk nor the prior served copy. So run the real case in a fresh session, or supply the file directly by path, which reads current. One real case is an illustration, not proof.

   Done when every difference between the run and the skill has been fixed in the skill, or you have reported that there were none.

## Diagnosing an existing skill

- **Never fires:** the description lacks the moment or the user's actual words. Sharpen the triggers.
- **Fires at the wrong time:** it overlaps another description. Write the boundary into both.
- **Followed only partly:** a step has a vague completion criterion, or the steps after it pull the agent forward. Sharpen the criterion first; split the sequence only if the rush still happens.
- **Too long:** move branch-only reference into sibling files, or split the skill by branch.

## Quality gates

- [ ] The description says what the skill does, then "Use when" with concrete moments; it does not restate the steps and names no owner, account or repo.
- [ ] No installed skill already covers it, and partial overlaps have written boundaries.
- [ ] SKILL.md is under 100 lines, every step has a completion criterion, and pointers are one level deep.
- [ ] Nothing in it is time-sensitive, terms are consistent, and owner-specific values live in `personal.md`.
- [ ] The user approved it before it was saved, and one real run matched the skill.
