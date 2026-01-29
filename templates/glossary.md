# Glossary Template

This template provides the structure for documenting internal terminology, codenames, acronyms, and jargon.

---

## Template Structure

```markdown
# [CODEBASE_NAME] Glossary

**Last Updated:** [DATE]

This glossary defines internal terminology, codenames, and acronyms used throughout the codebase. Terms are organized
alphabetically within categories.

---

## How to Use This Glossary

- **Ctrl+F** to find specific terms
- Terms in **bold** are internal codenames (vs. industry-standard terms)
- Links point to relevant documentation or code
- "See also" suggests related terms

---

## Internal Codenames & Components

These are names that won't appear in external documentation—you need to know them to read the code and communicate
with the team.

| Name             | What It Actually Is         | Code Location  |
|------------------|-----------------------------|----------------|
| **[CODENAME_1]** | [Plain-English description] | `[directory/]` |
| **[CODENAME_2]** | [Plain-English description] | `[directory/]` |
| **[CODENAME_3]** | [Plain-English description] | `[directory/]` |

---

## Acronyms

| Acronym      | Expansion   | Description         |
|--------------|-------------|---------------------|
| [ACRONYM_1]  | [Full Name] | [Brief description] |
| [ACRONYM_2]  | [Full Name] | [Brief description] |
| [ACRONYM_3]  | [Full Name] | [Brief description] |

---

## Technical Terms

### A

**[TERM_A1]**
[Definition. Include context about how this term is used in this specific codebase, which may differ from general
industry usage.]
*See also: [RELATED_TERM]*

**[TERM_A2]**
[Definition]

### B

**[TERM_B1]**
[Definition]

[Continue alphabetically...]

---

## Product/Domain Terms

[Terms specific to the product domain, not technical implementation]

| Term           | Definition                              |
|----------------|-----------------------------------------|
| [DOMAIN_TERM_1]| [What it means in this product context] |
| [DOMAIN_TERM_2]| [What it means in this product context] |

---

## Deprecated/Legacy Terms

[Terms you might encounter in older code or docs that are no longer current]

| Old Term   | Current Equivalent | Notes               |
|------------|-------------------|---------------------|
| [OLD_NAME] | [NEW_NAME]        | [When/why it changed]|

---

## External Technologies

[Brief definitions of external technologies used, with links to their docs]

| Technology | What It Is           | Our Usage        | Docs   |
|------------|----------------------|------------------|--------|
| [TECH_1]   | [One-line description]| [How we use it] | [Link] |
| [TECH_2]   | [One-line description]| [How we use it] | [Link] |

---

## Team/Org Terms

[If relevant, terms for teams, org structures, or processes]

| Term         | Meaning             |
|--------------|---------------------|
| [TEAM_TERM_1]| [What it refers to] |
| [TEAM_TERM_2]| [What it refers to] |
```

---

## Writing Tips

1. **Prioritize internal names** — Industry-standard terms can be Googled; internal codenames cannot

2. **Include the "why" when useful** — "Called 'Phoenix' because it rose from the ashes of the old CI system"

3. **Link to code locations** — Makes the glossary actionable

4. **Note deprecated terms** — Old docs and comments will use them

5. **Be concise** — This is a reference doc; 1-2 sentences per term is usually enough

6. **Update as you go** — Add terms as you discover them during exploration

7. **Cross-reference** — "See also" links help readers discover related concepts

---

## Discovery Tips

To find internal terminology during exploration:

1. **Check README files** — Often define key terms
2. **Look at class/function names** — Unusual names are often codenames
3. **Search for "aka" or "also known as"** — Code comments often explain names
4. **Check config files** — Component names, feature flags often use internal terms
5. **Look at directory names** — Non-obvious directory names are candidates
6. **Ask about ALL_CAPS names** — Often acronyms that need expansion
