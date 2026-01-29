# Product Overview Template

This template provides the structure for explaining WHY an area exists and what problems it solves. The key
differentiator is the **story walkthrough** that opens the document.

---

## Template Structure

```markdown
# [AREA_NAME]: Product Overview

**Last Updated:** [DATE]

## The Story: [DESCRIPTIVE_TITLE]

[Write a realistic scenario that illustrates why this area exists. The story should:]
- Feature a relatable protagonist (developer, data scientist, analyst, etc.)
- Present a real problem they face
- Show what the problem looks like in practice
- Walk through how this product/area addresses it
- Stay grounded and factual

[Example structure below — adapt to your area]

---

A [ROLE] at a [COMPANY_TYPE] needs to [TASK]. [DESCRIBE THEIR SITUATION].

**Before: [PROBLEM_TITLE]**

[Describe the situation without this solution:]
- [Challenge 1]
- [Challenge 2]
- [Challenge 3]

[Explain why existing approaches fall short]

**With [PRODUCT]: [SOLUTION_TITLE]**

[Walk through the solution, step by step:]

1. **[Step 1 title]**: [What they do and what happens]
2. **[Step 2 title]**: [What they do and what happens]
3. **[Step 3 title]**: [What they do and what happens]

[Continue the narrative through the workflow]

**Result**

[Describe the outcome. Include concrete details like:]
- Time saved
- Errors avoided
- Scale achieved
- Workflow improvements

---

## Core Concepts

[After the story, provide structured reference material]

### [CONCEPT_1]

**What it is:** [One-line definition]

**Why it matters:** [Why a developer needs to understand this]

**How it works:** [Brief technical explanation]

### [CONCEPT_2]

[Repeat pattern]

---

## Key Features

| Feature      | Description   | When to Use |
|--------------|---------------|-------------|
| [FEATURE_1]  | [Description] | [Use case]  |
| [FEATURE_2]  | [Description] | [Use case]  |

---

## Architecture at a Glance

[High-level diagram showing major components — keep it simple]

```
[USER] → [COMPONENT_1] → [COMPONENT_2] → [OUTCOME]
```

For detailed architecture, see [Codebase Overview](./codebase_overview.md).

---

## Common Use Cases

### [USE_CASE_1]

**Scenario:** [Brief description]

**Solution:** [How this area addresses it]

### [USE_CASE_2]

[Repeat pattern]

---

## What's NOT Covered Here

[Be explicit about boundaries]

- [Out of scope item 1] — See [LINK] instead
- [Out of scope item 2] — Handled by [OTHER_AREA]

---

## Related Documentation

- [Codebase Overview](./codebase_overview.md) — Technical architecture and components
- [Main Overview](../[main_overview].md) — Full codebase map
- [Glossary](../glossary.md) — Terminology
- [Existing docs in codebase] — [Link to any README or docs that exist for this area]

---

## Documentation Scope

This document explains *why* [AREA_NAME] exists and what problems it solves. It provides context for understanding
the area's purpose but does not cover implementation details.

**To go deeper:** See [Codebase Overview](./codebase_overview.md) for architecture, or ask for detailed documentation
on specific components or flows.
```

---

## Story Writing Tips

1. **Be specific** — "A data engineer at an e-commerce company" is clearer than "a user"

2. **Use realistic timelines** — "Week 1... Week 2... Month later" shows progression

3. **Show what goes wrong** — Describe the actual failure modes developers encounter

4. **Keep it professional** — Factual and direct. Avoid hyperbole, emotional language, or scare tactics.

5. **Ground in real problems** — "Data is spread across three systems" > "data discovery challenges"

6. **Show before/after** — Clear contrast between approaches, without exaggeration

7. **Include concrete numbers** — "50 TB", "45 minutes", "3 retries" make it tangible

8. **Connect to outcomes** — What does success look like in practice?

9. **Link to existing docs** — If the codebase has documentation for this area, reference it.

---

## Example Story Openings

**For an Auth System:**
> A security incident requires revoking a user's access across 47 different systems. With the current setup, an
> administrator opens each admin panel individually...

**For a Data Pipeline:**
> A report requires yesterday's sales data, but the numbers live in three different systems. The nightly ETL job
> failed, and the error logs don't indicate why...

**For an ML Platform:**
> A model achieves 94% accuracy in development. When the team attempts to deploy it to production, they discover
> the serving infrastructure requires a different model format...

**For a Monitoring System:**
> An alert fires: "Latency spike detected." The dashboard shows 47 different graphs. Determining which service is
> the root cause requires correlating data across multiple views...
