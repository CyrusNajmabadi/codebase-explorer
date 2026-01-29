# Main Overview Template

This template provides the structure for the entry-point document that maps the entire codebase.

---

## Template Structure

```markdown
# [CODEBASE_NAME] Codebase Overview

**Last Updated:** [DATE]
**Purpose:** High-level map of the [CODEBASE_NAME] codebase for engineers new to the project

---

## Table of Contents

1. [Quick Orientation](#quick-orientation)
2. [Product Areas](#product-areas)
3. [How to Use This Documentation](#how-to-use-this-documentation)

---

## Quick Orientation

### What is [PRODUCT_NAME]?

[2-3 paragraphs explaining what this codebase builds. Write for someone who has never heard of this product. Include:]
- What problem does it solve?
- Who uses it?
- What makes it technically interesting?

### Codebase at a Glance

| Metric                 | Value                  |
|------------------------|------------------------|
| Top-level directories  | [NUMBER]               |
| Primary languages      | [LANGUAGES]            |
| Build system           | [BUILD_SYSTEM]         |
| Repo type              | [Monorepo / Multi-repo]|

### Key Technologies

[Brief list of major technologies used, with links to external docs]

- **[TECH_1]** — [One-line description]
- **[TECH_2]** — [One-line description]
- ...

---

## Product Areas

[For each major area, include a brief description and links to detailed docs]

### [AREA_1_NAME]

**Purpose:** [One-line description]

**Why it matters:** [1-2 sentences on why a developer should care about this area]

**Key Directories:**
- `[dir1/]` — [Description]
- `[dir2/]` — [Description]

**Documentation:**
- [Product Overview](./[area_folder]/product_overview.md) — Why it exists, user scenarios
- [Codebase Overview](./[area_folder]/codebase_overview.md) — Architecture, components, patterns

---

### [AREA_2_NAME]

[Repeat pattern for each area]

---

## How to Use This Documentation

### If you're brand new
1. Read this overview to understand the landscape
2. Check the [Glossary](./glossary.md) for unfamiliar terms
3. Pick an area relevant to your work and read its Product Overview first

### If you're looking for something specific
- **"What is X?"** → Check the [Glossary](./glossary.md)
- **"Where is code for Y?"** → Check the relevant area's Codebase Overview
- **"What technology does Z use?"** → Check [Technology Mapping](./technology_mapping.md)

### If you're debugging
- Start with the area's Codebase Overview for architecture context
- Check Request Flow docs if tracing a specific path

---

## Related Documents

- [Glossary](./glossary.md) — All internal terms and acronyms
- [Technology Mapping](./technology_mapping.md) — What tech is used where
- [Build System](./build_system/overview.md) — How code is built (if applicable)
- [Test Infrastructure](./test_infrastructure/overview.md) — How code is tested (if applicable)
```

---

## Writing Tips

1. **The Quick Orientation matters most** — Many readers won't go further. Make it count.

2. **Be consistent in area descriptions** — Same structure for each area helps scanning.

3. **Include "Why it matters"** — Helps readers prioritize what to learn.

4. **Keep the Table of Contents updated** — It's how people navigate.

5. **Link generously** — This is a hub document; its value is in connecting to details.
