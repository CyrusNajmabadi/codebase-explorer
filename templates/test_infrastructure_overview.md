# Test Infrastructure Overview Template

This template provides the structure for documenting how code is tested, including test frameworks, patterns, and
infrastructure.

---

## Template Structure

```markdown
# [CODEBASE_NAME] Test Infrastructure Overview

| | |
|---|---|
| **Last Updated** | [DATE] |
| **Git SHA** | `[COMMIT_SHA]` |

This document explains how code is tested in the [CODEBASE_NAME] codebase, including test types, frameworks, and
best practices.

---

## Testing at a Glance

| Aspect                      | Approach    |
|-----------------------------|-------------|
| Unit test framework         | [FRAMEWORK] |
| Integration test framework  | [FRAMEWORK] |
| E2E test framework          | [FRAMEWORK] |
| Test runner                 | [RUNNER]    |
| Coverage tool               | [TOOL]      |

---

## Test Types

### Unit Tests

**What they test:** Individual functions/classes in isolation

**Framework:** [FRAMEWORK]

**Location pattern:** `[PATTERN, e.g., src/test/*, *.test.ts]`

**How to run:**
```bash
[COMMAND]
```

**Example:**
```[language]
// Example unit test structure
```

### Integration Tests

**What they test:** Multiple components working together

**Framework:** [FRAMEWORK]

**Location pattern:** `[PATTERN]`

**How to run:**
```bash
[COMMAND]
```

**Special setup required:** [Any databases, services, etc.]

### End-to-End Tests

**What they test:** Full user flows

**Framework:** [FRAMEWORK]

**Location pattern:** `[PATTERN]`

**How to run:**
```bash
[COMMAND]
```

**Environment requirements:** [What needs to be running]

---

## Test Frameworks by Language

### [LANGUAGE_1]

| Type        | Framework   | Assertion Library | Mocking    |
|-------------|-------------|-------------------|------------|
| Unit        | [FRAMEWORK] | [LIBRARY]         | [MOCK_LIB] |
| Integration | [FRAMEWORK] | [LIBRARY]         | [MOCK_LIB] |

**Common patterns:**
- [Pattern 1]
- [Pattern 2]

### [LANGUAGE_2]

[Repeat pattern]

---

## Running Tests

### Quick Reference

| Task                        | Command     |
|-----------------------------|-------------|
| Run all tests               | `[COMMAND]` |
| Run specific test file      | `[COMMAND]` |
| Run tests for changed files | `[COMMAND]` |
| Run with coverage           | `[COMMAND]` |
| Run in watch mode           | `[COMMAND]` |

### Filtering Tests

```bash
# Run tests matching a pattern
[COMMAND]

# Run tests in a specific directory
[COMMAND]

# Run a single test case
[COMMAND]
```

---

## Test Infrastructure

### Test Databases/Services

| Service      | Purpose                  | How to Start |
|--------------|--------------------------|--------------|
| [SERVICE_1]  | [What tests use it for]  | `[COMMAND]`  |
| [SERVICE_2]  | [What tests use it for]  | `[COMMAND]`  |

### Test Fixtures

**Location:** `[PATH]`

**Types:**
- [FIXTURE_TYPE_1]: [Description]
- [FIXTURE_TYPE_2]: [Description]

### Mocking Patterns

**[PATTERN_1_NAME]:**
```[language]
// Example code
```

**[PATTERN_2_NAME]:**
```[language]
// Example code
```

---

## CI Test Execution

### How Tests Run in CI

```
[VISUAL REPRESENTATION OF CI TEST FLOW]
```

### Test Parallelization

[How tests are split across CI workers]

### Flaky Test Handling

| Mechanism      | Description     |
|----------------|-----------------|
| [MECHANISM_1]  | [How it works]  |
| [MECHANISM_2]  | [How it works]  |

### Test Failure Investigation

When a test fails in CI:
1. [Step 1]
2. [Step 2]
3. [Step 3]

---

## Coverage

### Coverage Requirements

| Area      | Minimum Coverage |
|-----------|------------------|
| [AREA_1]  | [PERCENTAGE]     |
| [AREA_2]  | [PERCENTAGE]     |

### Generating Coverage Reports

```bash
[COMMAND]
```

### Coverage Exclusions

[What's intentionally excluded from coverage and why]

---

## Writing Good Tests

### Do

- [Best practice 1]
- [Best practice 2]
- [Best practice 3]

### Don't

- [Anti-pattern 1]
- [Anti-pattern 2]
- [Anti-pattern 3]

### Naming Conventions

```
[NAMING_PATTERN_EXPLANATION]
```

---

## Debugging Tests

### Common Issues

| Issue      | Cause  | Solution |
|------------|--------|----------|
| [ISSUE_1]  | [Why]  | [Fix]    |
| [ISSUE_2]  | [Why]  | [Fix]    |

### Debugging Tools

- [TOOL_1]: [How to use it]
- [TOOL_2]: [How to use it]

---

## Key Directories

| Directory | Contents                 |
|-----------|--------------------------|
| `[DIR_1]` | [Test utilities]         |
| `[DIR_2]` | [Test fixtures]          |
| `[DIR_3]` | [CI test configuration]  |

---

## Related Documentation

- [Build System](./build_system/overview.md)
- [Main Overview](./[main_overview].md)
```

---

## Writing Tips

1. **Make commands copy-pasteable** — Include full commands, not fragments

2. **Document flaky test handling** — Every codebase has them

3. **Include debugging guidance** — What to do when tests fail

4. **Show real examples** — Abstract patterns + concrete examples

5. **Document test data/fixtures** — Where to find them, how to create them

6. **Explain CI behavior** — Local vs CI differences cause confusion
