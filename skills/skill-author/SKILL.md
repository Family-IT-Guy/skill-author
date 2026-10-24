---
name: skill-author
description: Create new agent skills with proper structure, progressive disclosure, and bundled resources. Use when user wants to create, write, or build a new skill.
---

# Writing Skills

Before drafting or editing a skill, load the `writing-great-skills` skill that ships in this plugin (`skill-author:writing-great-skills`, through the Skill tool; its `GLOSSARY.md` holds the full definitions) for the quality vocabulary and principles — predictability, leading words, the information-hierarchy ladder, progressive disclosure, and the failure modes (premature completion, duplication, sediment, sprawl, no-op) — and apply them throughout.

## Process

1. **Gather requirements** - ask user about:
   - What task/domain does the skill cover?
   - What specific use cases should it handle?
   - Does it need executable scripts or just instructions?
   - Any reference materials to include?

2. **Draft the skill** - create:
   - SKILL.md with concise instructions
   - Additional reference files if content exceeds 500 lines
   - Utility scripts if deterministic operations needed

3. **Review with user** - present draft and ask:
   - Does this cover your use cases?
   - Anything missing or unclear?
   - Should any section be more/less detailed?

4. **Run it once before trusting it** - a draft is a hypothesis about what an agent will do, and reading it cannot test that. Put the skill in front of an agent **the way it will actually be reached** - invoke it if it is model-invoked, or supply the file if it carries `disable-model-invocation` and is reached by a path - then give one real case, not a hypothetical, and compare what the agent does against what the skill says. Where they differ, the skill is the thing that changes.

   This catches the one failure review cannot: a skill can read correctly and still not produce the behaviour it describes. One real case, once, is the bar - this is not a full test methodology. It applies to EDITS as well as new skills, which is where it is most often skipped.

   **A skill edited mid-session does not reach the agent that edited it.** Measured once: this step was added, then revised, then the skill was invoked - and the harness served the revision before it, matching neither the disk nor the prior served copy exactly. So an edit verified by re-invoking in the same session verifies a stale copy. Run the real case in a FRESH session, or supply the file directly by path, which reads current.

## Skill Structure

```
skill-name/
├── SKILL.md           # Main instructions (required)
├── REFERENCE.md       # Detailed docs (if needed)
├── EXAMPLES.md        # Usage examples (if needed)
└── scripts/           # Utility scripts (if needed)
    └── helper.js
```

## SKILL.md Template

```md
---
name: skill-name
description: Brief description of capability. Use when [specific triggers].
---

# Skill Name

## Quick start

[Minimal working example]

## Workflows

[Step-by-step processes with checklists for complex tasks]

## Advanced features

[Link to separate files: See [REFERENCE.md](REFERENCE.md)]
```

## Description Requirements

The description is **the only thing your agent sees** when deciding which skill to load. It's surfaced in the system prompt alongside all other installed skills. Your agent reads these descriptions and picks the relevant skill based on the user's request.

**Goal**: Give your agent just enough info to know:

1. What capability this skill provides
2. When/why to trigger it (specific keywords, contexts, file types)

**Format**:

- Max 1024 chars
- Write in third person
- First sentence: what it does
- Second sentence: "Use when [specific triggers]"
- Do NOT summarize the skill's workflow or steps in the description. If the description restates the process, the agent follows it and never reads the skill body. Keep it to capability + triggers.

**This section is the only rule on descriptions.** A widely installed skill, `superpowers:writing-skills`, fires on this same moment and says the opposite — *"CRITICAL: Description = When to Use, NOT What the Skill Does"* — against the format above, which puts what it does first and the triggers second. If both are installed, this section wins.

**Good example**:

```
Extract text and tables from PDF files, fill forms, merge documents. Use when working with PDF files or when user mentions PDFs, forms, or document extraction.
```

**Bad example**:

```
Helps with documents.
```

The bad example gives your agent no way to distinguish this from other document skills.

## When to Add Scripts

Add utility scripts when:

- Operation is deterministic (validation, formatting)
- Same code would be generated repeatedly
- Errors need explicit handling

Scripts save tokens and improve reliability vs generated code.

## When to Split Files

Split into separate files when:

- SKILL.md exceeds 100 lines
- Content has distinct domains (finance vs sales schemas)
- Advanced features are rarely needed

## Review Checklist

After drafting, verify:

- [ ] Description includes triggers ("Use when...")
- [ ] Description does NOT restate the skill's workflow/steps
- [ ] SKILL.md under 100 lines
- [ ] No time-sensitive info
- [ ] Consistent terminology
- [ ] Concrete examples included
- [ ] References one level deep
- [ ] Run on one real case; what the agent did matches what the skill says
