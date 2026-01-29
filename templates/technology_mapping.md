# Technology Mapping Template

This template provides the structure for documenting which technologies are used where across the codebase.

---

## Template Structure

```markdown
# [CODEBASE_NAME] Technology Mapping

**Last Updated:** [DATE]

This document maps technologies to their usage across the codebase. Use it to answer "where is X used?" and "what
tech does Y use?"

---

## Technology by Category

### Languages

| Language | Primary Use    | Key Areas              |
|----------|----------------|------------------------|
| [LANG_1] | [Main purpose] | `[dir1/]`, `[dir2/]`   |
| [LANG_2] | [Main purpose] | `[dir3/]`, `[dir4/]`   |

### Frameworks

| Framework      | Purpose            | Where Used         |
|----------------|--------------------|--------------------|
| [FRAMEWORK_1]  | [What it provides] | [Areas/components] |
| [FRAMEWORK_2]  | [What it provides] | [Areas/components] |

### Databases

| Database | Purpose          | Used By            |
|----------|------------------|--------------------|
| [DB_1]   | [What it stores] | [Components/Areas] |
| [DB_2]   | [What it stores] | [Components/Areas] |

### Messaging & Streaming

| Technology | Purpose              | Used By            |
|------------|----------------------|--------------------|
| [MSG_1]    | [What flows through] | [Components/Areas] |
| [MSG_2]    | [What flows through] | [Components/Areas] |

### Infrastructure

| Technology | Purpose        | Where Used |
|------------|----------------|------------|
| [INFRA_1]  | [What it does] | [Areas]    |
| [INFRA_2]  | [What it does] | [Areas]    |

---

## Area-by-Area Technology Stack

### [AREA_1]

| Layer     | Technology       |
|-----------|------------------|
| Language  | [LANG]           |
| Framework | [FRAMEWORK]      |
| Database  | [DB]             |
| Messaging | [MSG]            |
| Testing   | [TEST_FRAMEWORK] |

### [AREA_2]

[Repeat pattern]

---

## Technology Usage Matrix

A quick-reference matrix showing which areas use which technologies.

| Technology | [Area 1] | [Area 2] | [Area 3] | [Area 4] | [Area 5] |
|------------|----------|----------|----------|----------|----------|
| [TECH_1]   | ✓        |          | ✓        |          | ✓        |
| [TECH_2]   |          | ✓        | ✓        | ✓        |          |
| [TECH_3]   | ✓        | ✓        |          |          | ✓        |
| [TECH_4]   |          |          | ✓        | ✓        |          |

---

## Technology Notes

### [TECH_1]

**Version:** [VERSION]

**Why it's used:** [Rationale for choosing this technology]

**Quirks:** [Anything unusual about how it's used here]

**Links:** [Documentation URL]

### [TECH_2]

[Repeat pattern for technologies that need explanation]

---

## Build & CI Technologies

| Technology | Purpose          |
|------------|------------------|
| [BUILD_1]  | [What it builds] |
| [CI_1]     | [What it runs]   |

---

## Deprecated Technologies

[Technologies being phased out—helpful for understanding legacy code]

| Technology | Replacement | Migration Status |
|------------|-------------|------------------|
| [OLD_TECH] | [NEW_TECH]  | [Status]         |
```

---

## Writing Tips

1. **Be specific about versions** — "Java 11" not just "Java"

2. **Explain non-obvious choices** — Why gRPC here but REST there?

3. **Include deprecated tech** — You'll encounter it in older code

4. **Link to external docs** — Don't re-explain well-documented tech

5. **The matrix is worth the effort** — Quick visual reference for "what uses what"

6. **Note quirks** — "We use Kafka but with a custom serializer because..."

---

## Discovery Tips

To find technology usage during exploration:

1. **Check build files** — `pom.xml`, `package.json`, `Cargo.toml`, `BUILD` reveal dependencies
2. **Look at imports** — What libraries are imported?
3. **Check docker/k8s configs** — What images are used?
4. **Search for connection strings** — Database/messaging URLs
5. **Look at CI configs** — What tools does CI use?
