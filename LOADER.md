# Codebase Explorer - Loader Prompts

This file contains prompts to start AI agent sessions for codebase exploration:
1. **Initial exploration** — First time exploring a codebase
2. **Expanding documentation** — Drilling deeper into an area with existing docs
3. **Verification** — Auditing existing documentation against current code

---

## Core Philosophy

All prompts in this file share the same philosophy:

**Living Documents**: This documentation should be a living, accurate representation of the codebase. Drift between docs and code is a failure state.

**Deep Verification**: Never do cursory checks or surface-level reviews. Read actual source code. Verify every significant claim. Don't trust git diffs as your only signal — diffs show what lines changed, not whether docs are accurate.

**Thoroughness Over Speed**: Be extremely thorough. Read the code. Trace data flows. Verify architectural claims against implementation. Use subagents to parallelize work across independent areas.

---

## Fetching the Methodology

All prompts require fetching the methodology. Use this block (replacing `[YOUR_USERNAME]`):

```
Please fetch the exploration methodology and templates from:
https://raw.githubusercontent.com/[YOUR_USERNAME]/codebase-explorer/main/

Specifically, fetch:
- README.md (the main methodology)
- LOADER.md (this file)
- All templates from /templates/:
  - main_overview.md, product_overview.md, codebase_overview.md
  - glossary.md, technology_mapping.md
  - build_system_overview.md, test_infrastructure_overview.md
  - component_catalog.md, request_flow.md
```

---

## Initial Exploration Prompt

Use this for first-time exploration of an unfamiliar codebase.

```
I need your help understanding a complex codebase I'm unfamiliar with.

[FETCH METHODOLOGY - see "Fetching the Methodology" section above]

Once loaded, begin exploring:

Codebase location: [PATH_OR_URL]
Output location: [WHERE_TO_SAVE_DOCS]
Methodology location: [URL_TO_THIS_REPO - so generated docs can reference it]

Any specific areas I care about: [OPTIONAL - e.g., "backend services" or "the ML pipeline"]
```

**Usage Notes:**
- Replace `[PATH_OR_URL]` with the codebase path (local) or repo URL
- Replace `[WHERE_TO_SAVE_DOCS]` with where you want documentation saved
- Replace `[URL_TO_THIS_REPO]` with the GitHub URL to this methodology repo
- The "specific areas" field is optional but helps prioritize

---

## Expanding Documentation Prompt

Use this when documentation already exists and you want to:
- Drill deeper into a specific area
- Update documentation after code changes
- Fill in gaps in existing coverage

```
I have a codebase with existing AI-generated documentation that I'd like to expand and verify.

[FETCH METHODOLOGY - see "Fetching the Methodology" section above]

Then:
1. Read the existing documentation at: [PATH_TO_DOCS_FOLDER]
2. Note the Git SHA recorded in the existing docs
3. Check what changed in the codebase since then (if git repo)
4. Start with the Main Overview and Glossary to understand current state
5. I'd like to drill deeper into: [SPECIFIC_AREA - e.g., "the parser component"]

IMPORTANT: This is not a surface-level update. Deeply verify ALL existing documentation
in this area still matches the code. Read actual source files. Update anything that has
drifted, even if git diffs don't obviously show it.
```

### What the Agent Should Do

1. Read existing docs and **note the Git SHA recorded**
2. **Deeply verify existing documentation**:
   - Read actual source code, not just git diffs
   - For each architectural claim, verify it's still true
   - Check data flows, component relationships, interfaces
   - Verify terminology and internal names haven't changed
   - Look for subtle drift: code that evolved while docs stayed static
3. **Update all inaccuracies**, whether from:
   - Code changes since docs were written
   - Original documentation that was incomplete
   - Terminology that has evolved
4. Explore the specified area in more depth
5. Create detailed documentation following the methodology
6. Update existing docs with links to new detailed docs
7. **Record the new Git SHA** in all new/updated documents

---

## Verification Agent Prompt

Use this when you want an independent agent — with no prior context — to audit existing
documentation against the current codebase.

**When to Use:**
- After major codebase changes (refactors, new versions)
- Periodically to catch drift
- When onboarding to documentation created by others
- Before relying on docs for critical decisions

```
I need you to perform a deep verification audit of existing codebase documentation.

CONTEXT:
A previous AI agent explored a codebase and generated documentation following the
Codebase Explorer methodology. Your job is to verify that documentation is accurate.

[FETCH METHODOLOGY - see "Fetching the Methodology" section above]

WHAT TO VERIFY:
- Codebase location: [PATH_OR_URL]
- Existing documentation: [PATH_TO_DOCS_FOLDER]
- Area to verify: [SPECIFIC_AREA or "all"]

YOUR TASK:

1. Read the existing documentation completely

2. For EACH significant claim:
   - Locate the relevant source code
   - Read and understand the actual implementation
   - Verify the claim is accurate and complete
   - Note any discrepancies, no matter how small

3. Specifically verify:
   - Architectural descriptions match actual code structure
   - Data flows described actually work that way
   - Component relationships are correctly documented
   - Internal terminology and names are current
   - Code examples (if any) are correct and functional
   - Cross-references between docs are valid

4. Check for drift patterns:
   - Code that evolved while docs stayed static
   - Features added that aren't documented
   - Features removed that are still documented
   - Subtle behavioral changes not reflected in docs

5. Produce a verification report (see template below)

6. If authorized, fix the documentation directly

Be extremely thorough. Small inaccuracies compound into misleading documentation.
If something seems off, investigate deeply rather than assuming it's fine.
```

### Verification Checklist

**Main Overview**
- [ ] Area categorization still makes sense
- [ ] All listed areas exist and are correctly described
- [ ] Technology stack is current

**Product Overviews**
- [ ] Features listed are actually implemented
- [ ] Architecture descriptions match code
- [ ] "What's NOT covered" sections are accurate

**Codebase Overviews**
- [ ] Directory structure matches actual structure
- [ ] Key files exist and do what's described
- [ ] Component interactions are correct
- [ ] Internal terminology matches code

**Glossary**
- [ ] All terms are still used
- [ ] Definitions match actual usage
- [ ] No significant terms missing

**Technology Mapping**
- [ ] Technologies listed are still in use
- [ ] Purposes described match actual usage

### Verification Report Template

```markdown
# Documentation Verification Report

| | |
|---|---|
| **Verified** | [DATE] |
| **Git SHA** | `[CURRENT_SHA]` |
| **Docs SHA** | `[SHA_FROM_DOCS]` |
| **Area** | [AREA_VERIFIED] |

## Summary

- **Documents verified**: [COUNT]
- **Issues found**: [COUNT]
- **Severity**: [CRITICAL/MODERATE/MINOR]

## Verified as Accurate

[List major claims verified correct]

## Discrepancies Found

### [Issue Title]
- **Document**: [path/to/doc.md]
- **Claim**: "[What the doc says]"
- **Reality**: "[What the code actually does]"
- **Severity**: [CRITICAL/MODERATE/MINOR]
- **Fix**: [What should change]

## Recommendations

[Overall recommendations]

## Files Examined

[List of source files read during verification]
```

---

## Alternative: No Network Access

If the agent can't fetch from GitHub, paste README.md contents directly, then say:

```
I've pasted the methodology above. The templates are in the /templates folder of the same repo.
The methodology repo is at: [URL_TO_THIS_REPO]

Please proceed with exploring [CODEBASE_PATH] and save documentation to [OUTPUT_PATH].
```

---

## What Generated Docs Should Include

Generated docs should reference this methodology so users know how to expand/verify later:

**In each "Documentation Scope" section:**
```markdown
## Documentation Scope

This documentation provides a high-level overview. For more detail or to verify accuracy:
- [Expanding Documentation Prompt](https://github.com/[USER]/codebase-explorer/blob/main/LOADER.md#expanding-documentation-prompt) — drill deeper into specific areas
- [Verification Prompt](https://github.com/[USER]/codebase-explorer/blob/main/LOADER.md#verification-agent-prompt) — audit documentation against current code
```

---

## Required AI Capabilities

This methodology works best with AI agents that can:
- **Read files** from the local filesystem or repository
- **Search/grep** through code
- **Write files** to create documentation
- **Execute commands** (optional, for build system exploration)
- **Parallel execution** (optional but faster)
- **Fetch URLs** (optional, for loading templates from GitHub)
- **Web search** (optional, for enriching documentation with links to official docs, technology sites, Wikipedia, etc. — use judiciously where links genuinely help readers)

Most modern AI coding assistants support these capabilities.
