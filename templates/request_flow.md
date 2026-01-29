# Data/Request Flow Template

This template provides the structure for documenting how data or requests flow through the system end-to-end. These
"trace a flow" documents are particularly useful for understanding how components connect.

**Works for:**
- HTTP/API requests through services
- Data transformation pipelines
- Compilation/build pipelines
- User actions through UI → backend → storage
- Any multi-step processing flow

---

## Choosing the Right Level of Detail

Flow documents work best when they match the reader's needs. A single flow document trying to cover everything
becomes overwhelming; too shallow and it's not useful.

### Hierarchical Approach (Recommended for Complex Systems)

For large systems like compilers, databases, or distributed platforms, create flows at multiple levels:

**Level 1: System-wide flow (5-10 steps)**
```
Source Text → Parser → Binder → Checker → Emitter → Output
```
Each step is a major phase. Links to Level 2 docs for details.

**Level 2: Phase-level flow (5-15 steps)**
```
Parser: Text → Lexer → Token Stream → Syntax Tree Builder → Syntax Tree
```
Each step is a component within the phase. Links to Level 3 if needed.

**Level 3: Component-level flow (as detailed as needed)**
```
Lexer: Character Stream → Token Recognition → Trivia Handling → Token Creation
```

### Guidance by Codebase Size

| Codebase Complexity | Approach |
|---------------------|----------|
| Small (< 10 components) | Single detailed flow document may suffice |
| Medium (10-50 components) | Top-level flow + detailed flows for key paths |
| Large (50+ components) | Hierarchical: system → area → component flows |

### Signs You're at the Wrong Level

**Too high-level:**
- Steps are entire subsystems with no explanation of what happens inside
- Reader still can't trace code after reading

**Too detailed:**
- Document is thousands of lines
- Covers every edge case and internal helper function
- Changes frequently as implementation details shift

**Right level:**
- Reader can follow along in the code
- Steps map to identifiable components or functions
- Document is stable across minor refactors

---

## Template Structure

```markdown
# [FLOW_TYPE] Flow: [FLOW_NAME]

**Last Updated:** [DATE]

This document traces [WHAT_IS_BEING_TRACED] through the system, showing which components are involved and how they
interact.

---

## Overview

**What we're tracing:** [Brief description—e.g., "a SQL query from user input to results", "source code from text to
compiled IL", "a click event from UI to state update"]

**Why this matters:** [Why understanding this flow is valuable]

**Key components involved:**
- [COMPONENT_1]
- [COMPONENT_2]
- [COMPONENT_3]

---

## Flow Diagram

[Choose the diagram style that fits your flow type]

### Service-Oriented Flow
```
┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
│  Client  │────▶│ Gateway  │────▶│ Service  │────▶│ Database │
└──────────┘     └──────────┘     └──────────┘     └──────────┘
```

### Pipeline/Transformation Flow
```
┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
│  Input   │────▶│ Stage 1  │────▶│ Stage 2  │────▶│  Output  │
│  (text)  │     │ (parse)  │     │(analyze) │     │  (IL)    │
└──────────┘     └──────────┘     └──────────┘     └──────────┘
```

### Layered Flow
```
┌─────────────────────────────────────┐
│         Presentation Layer          │
└─────────────────┬───────────────────┘
                  ▼
┌─────────────────────────────────────┐
│          Business Layer             │
└─────────────────┬───────────────────┘
                  ▼
┌─────────────────────────────────────┐
│           Data Layer                │
└─────────────────────────────────────┘
```

---

## Step-by-Step Walkthrough

### Step 1: [STEP_TITLE]

**Component:** [COMPONENT_NAME]
**Code location:** `[file/path.ext]`

**What happens:**
1. [Detailed action 1]
2. [Detailed action 2]
3. [Detailed action 3]

**Key code:**
```[language]
// Relevant code snippet (simplified)
```

**Data at this point:**
```json
{
  "field": "value",
  "state": "description"
}
```

**Next:** Passes to [NEXT_COMPONENT] via [PROTOCOL]

---

### Step 2: [STEP_TITLE]

**Component:** [COMPONENT_NAME]
**Code location:** `[file/path.ext]`

**What happens:**
[Detailed explanation]

**Decision point:**
- If [CONDITION_A]: [PATH_A]
- If [CONDITION_B]: [PATH_B]
- Otherwise: [DEFAULT_PATH]

**Next:** [NEXT_COMPONENT]

---

### Step 3: [STEP_TITLE]

[Continue pattern for each step]

---

## Error Handling

### What happens if [FAILURE_SCENARIO_1]?

**Detection:** [How the error is detected]

**Handling:** [What the system does]

**User experience:** [What the user sees]

**Recovery:** [How to recover]

### What happens if [FAILURE_SCENARIO_2]?

[Repeat pattern]

---

## Timing & Performance

| Step      | Typical Duration | Notes       |
|-----------|------------------|-------------|
| Step 1    | [TIME]           | [Any notes] |
| Step 2    | [TIME]           | [Any notes] |
| Step 3    | [TIME]           | [Any notes] |
| **Total** | **[TOTAL]**      |             |

**Bottlenecks:** [Where time is typically spent]

**Optimization opportunities:** [Potential improvements]

---

## Variations

### [VARIATION_1_NAME]

**When it applies:** [Condition]

**How it differs:** [What changes in the flow]

### [VARIATION_2_NAME]

[Repeat pattern]

---

## Observability

### Logging

| Step   | Log Location | Key Fields |
|--------|--------------|------------|
| Step 1 | [WHERE]      | `[FIELDS]` |
| Step 2 | [WHERE]      | `[FIELDS]` |

### Metrics

| Metric       | What It Measures |
|--------------|------------------|
| `[METRIC_1]` | [Description]    |
| `[METRIC_2]` | [Description]    |

### Tracing

**Trace ID propagation:** [How trace context flows through]

**Key spans:** [Important spans to look for]

---

## Common Issues & Debugging

### "[SYMPTOM_1]"

**Likely cause:** [Explanation]

**How to debug:**
1. [Step 1]
2. [Step 2]
3. [Step 3]

### "[SYMPTOM_2]"

[Repeat pattern]

---

## Related Flows

**More detailed (drill down):**
- [Step 2 Detailed Flow](./[link].md) — Expands on [STEP_2] in detail

**Same level (parallel flows):**
- [Related Flow 1](./[link].md) — [How it relates]

**Higher level (zoom out):**
- [System Overview Flow](./[link].md) — Where this flow fits in the bigger picture

---

## Related Documentation

- [Component A Overview](./[link].md)
- [Component B Overview](./[link].md)
- [Main Overview](./[main_overview].md)
```

---

## Writing Tips

1. **Pick the right level of detail** — Start with high-level flows; add detailed sub-flows as needed. Link between
   levels rather than cramming everything into one document.

2. **Pick meaningful flows** — User login, data write, query execution, not obscure edge cases

3. **Be specific about code locations** — "Check `AuthService.validate()`" > "the auth service validates"

4. **Include actual data shapes** — Show what the request/response looks like

5. **Cover error paths** — Happy path is easy; errors are where people get stuck

6. **Add timing information** — Helps with performance debugging

7. **Show decision points** — Where does the flow branch?

8. **Make it traceable** — Include enough detail that someone can follow along in the code

---

## Good Flow Candidates

### For Service-Oriented Codebases
- User authentication/login
- Primary data operations (create, read, update, delete)
- Payment/billing flows
- API request handling
- Background job execution

### For Compiler/Language Toolchains
- Source text → Syntax tree → Semantic model → Output
- Error detection and reporting flow
- IDE feature flow (e.g., "Go to Definition")
- Incremental compilation/caching

### For Library/SDK Codebases
- Public API → Internal implementation → Result
- Extension/plugin loading and execution
- Configuration loading and validation

### For Data Processing Systems
- Data ingestion → Transformation → Output
- Query parsing → Optimization → Execution
- Streaming data through pipeline stages

### Generally Less Valuable
- Rarely-used admin operations
- One-off migration scripts
- Internal health checks
- Initialization/bootstrap (unless complex)
