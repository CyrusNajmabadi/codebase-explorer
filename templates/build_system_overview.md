# Build System Overview Template

This template provides the structure for documenting how code is built, including build tools, CI/CD, and developer
workflows.

---

## Template Structure

```markdown
# [CODEBASE_NAME] Build System Overview

| | |
|---|---|
| **Last Updated** | [DATE] |
| **Git SHA** | `[COMMIT_SHA]` |

This document explains how code is built, tested, and deployed in the [CODEBASE_NAME] codebase.

---

## Build System at a Glance

| Aspect                  | Technology/Approach |
|-------------------------|---------------------|
| Primary build tool      | [TOOL]              |
| Language-specific tools | [TOOLS]             |
| CI system               | [SYSTEM]            |
| Artifact storage        | [WHERE]             |
| Deployment              | [HOW]               |

---

## Core Build Tool: [BUILD_TOOL]

### Why [BUILD_TOOL]?

[Explain the rationale for choosing this build system]
- [Reason 1]
- [Reason 2]
- [Reason 3]

### Basic Commands

| Task                  | Command     |
|-----------------------|-------------|
| Build all             | `[COMMAND]` |
| Build specific target | `[COMMAND]` |
| Run tests             | `[COMMAND]` |
| Clean                 | `[COMMAND]` |

### Key Concepts

**[CONCEPT_1]:** [Explanation of a build system concept specific to this codebase]

**[CONCEPT_2]:** [Another concept]

### Build Configuration

| File              | Purpose              |
|-------------------|----------------------|
| `[CONFIG_FILE_1]` | [What it configures] |
| `[CONFIG_FILE_2]` | [What it configures] |

---

## Language-Specific Tooling

### [LANGUAGE_1]

**Build tool:** [TOOL]
**Package manager:** [MANAGER]
**Key commands:**
- `[COMMAND_1]` — [Purpose]
- `[COMMAND_2]` — [Purpose]

### [LANGUAGE_2]

[Repeat pattern]

---

## CI/CD Pipeline

### Pipeline Overview

```
[TRIGGER] → [STAGE_1] → [STAGE_2] → [STAGE_3] → [DEPLOY]
```

### Stages

| Stage      | Purpose        | Duration       |
|------------|----------------|----------------|
| [STAGE_1]  | [What it does] | [Typical time] |
| [STAGE_2]  | [What it does] | [Typical time] |
| [STAGE_3]  | [What it does] | [Typical time] |

### CI Configuration

- **Config location:** `[PATH]`
- **Runner type:** [Self-hosted/Cloud]
- **Parallelization:** [How tests are split]

### Common CI Issues

| Issue      | Cause             | Solution      |
|------------|-------------------|---------------|
| [ISSUE_1]  | [Why it happens]  | [How to fix]  |
| [ISSUE_2]  | [Why it happens]  | [How to fix]  |

---

## Developer Workflow

### First-Time Setup

1. [Step 1]
2. [Step 2]
3. [Step 3]

### Daily Workflow

**Making changes:**
```bash
# [Command sequence for typical development]
```

**Before committing:**
```bash
# [Pre-commit checks]
```

**Submitting for review:**
```bash
# [PR/review process]
```

### Pre-commit Hooks

| Hook      | Purpose           |
|-----------|-------------------|
| [HOOK_1]  | [What it checks]  |
| [HOOK_2]  | [What it checks]  |

---

## Build Performance

### Caching

| Cache Type | Purpose           | Location |
|------------|-------------------|----------|
| [CACHE_1]  | [What it caches]  | [Where]  |
| [CACHE_2]  | [What it caches]  | [Where]  |

### Optimization Tips

- [Tip 1 for faster builds]
- [Tip 2 for faster builds]
- [Tip 3 for faster builds]

---

## Troubleshooting

### "Build is slow"

[Common causes and solutions]

### "Build fails with [ERROR]"

[Common errors and fixes]

### "CI is red but local passes"

[Environment differences to check]

---

## Key Directories

| Directory | Purpose               |
|-----------|-----------------------|
| `[DIR_1]` | [Build configuration] |build_
| `[DIR_2]` | [CI configuration]    |
| `[DIR_3]` | [Build tooling/scripts]|

---

## Related Documentation

- [Test Infrastructure](./test_infrastructure/overview.md)
- [Main Overview](./[main_overview].md)
```

---

## Writing Tips

1. **Commands should be copy-pasteable** — Test them before documenting

2. **Include timing expectations** — "This takes ~5 minutes" sets expectations

3. **Document common failures** — Saves hours of debugging

4. **Explain the "why"** — Why Bazel? Why this CI system?

5. **Keep first-time setup current** — Outdated setup docs cause the most friction

6. **Include optimization tips** — Faster builds improve everyone's workflow
