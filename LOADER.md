# Codebase Explorer - Loader Prompts

This file contains prompts to start AI agent sessions for codebase exploration. There are three main scenarios:
1. **Initial exploration** — First time exploring a codebase
2. **Expanding documentation** — Drilling deeper into an area that already has high-level docs
3. **Verification** — Deeply auditing existing documentation against current code

---

## Initial Exploration Prompt

Copy and paste this into a new AI agent session to begin exploring an unfamiliar codebase.

```
I need your help understanding a complex codebase I'm unfamiliar with.

Please fetch the exploration methodology and templates from:
https://raw.githubusercontent.com/[YOUR_USERNAME]/codebase-explorer/main/

Specifically, fetch:
- README.md (the main methodology)
- LOADER.md (this file - so you know how to reference it in generated docs)
- All templates from /templates/:
  - main_overview.md
  - product_overview.md
  - codebase_overview.md
  - glossary.md
  - technology_mapping.md
  - build_system_overview.md
  - test_infrastructure_overview.md
  - component_catalog.md
  - request_flow.md

Once loaded, begin exploring:

Codebase location: [PATH_OR_URL]
Output location: [WHERE_TO_SAVE_DOCS]
Methodology location: [URL_TO_THIS_REPO - so generated docs can reference it]

Any specific areas I care about: [OPTIONAL - e.g., "backend services" or "the ML pipeline"]
```

### Usage Notes

1. Replace `[YOUR_USERNAME]` with your GitHub username (or org name)
2. Replace `[PATH_OR_URL]` with the codebase path (local) or repo URL
3. Replace `[WHERE_TO_SAVE_DOCS]` with where you want documentation saved
4. Replace `[URL_TO_THIS_REPO]` with the GitHub URL (e.g., `https://github.com/yourname/codebase-explorer`)
5. The "specific areas" field is optional but helps prioritize

---

## Expanding Documentation Prompt

Use this when documentation already exists (from a previous session) and you want to drill deeper into a specific
area, or when code has changed and documentation needs updating.

**Philosophy: Living Documents**

This documentation is meant to be a living, accurate representation of the codebase. When you run this prompt:
- You are not doing a cursory check or surface-level review
- You are deeply verifying that all existing documentation remains accurate
- You have hours to run — use them to be thorough
- Every claim in the docs should be verified against actual code
- Significant drift between docs and code is a failure state

```
I have a codebase with existing AI-generated documentation that I'd like to expand and verify.

Please fetch the exploration methodology and templates from:
https://raw.githubusercontent.com/[YOUR_USERNAME]/codebase-explorer/main/

Specifically, fetch:
- README.md (the main methodology)
- LOADER.md (for reference)
- All templates from /templates/

Then:
1. Read the existing documentation at: [PATH_TO_DOCS_FOLDER]
2. Note the Git SHA recorded in the existing docs
3. Check what changed in the codebase since the docs were generated (if this is a git repo)
4. Start with the Main Overview and Glossary to understand what's already documented
5. I'd like to drill deeper into: [SPECIFIC_AREA - e.g., "the parser component" or "authentication flow"]

IMPORTANT: This is not a surface-level update. You should:
- Deeply verify ALL existing documentation in this area still matches the code
- Read the actual source files, not just git diffs
- Check that architectural descriptions, data flows, and concepts are still accurate
- Update anything that has drifted, even if the git diff doesn't obviously show it
- You have hours to run — be thorough

Please create detailed documentation for that area, linking back to the existing high-level docs.
```

### What the Agent Should Do

1. Fetch and read the methodology (README.md) and templates
2. Read existing documentation to understand current state and **note the Git SHA recorded in the docs**
3. **Deeply verify existing documentation** (this is critical):
   - Don't just look at git diffs — read the actual source code
   - For each major concept or architectural claim in the docs, verify it's still true
   - Check that data flows, component relationships, and interfaces are accurately described
   - Verify that terminology and internal names haven't changed
   - Look for subtle drift: code that evolved while docs stayed static
4. **Check what changed since last documentation** (if git repo):
   - Get current SHA: `git rev-parse HEAD`
   - Compare to SHA in docs: `git diff --stat OLD_SHA..HEAD -- path/to/area/`
   - But don't rely solely on diffs — diffs show what lines changed, not whether docs are accurate
   - A file with no changes might still have docs that were always slightly wrong
5. **Update all inaccuracies**, whether caused by:
   - Code changes since the docs were written
   - Original documentation that was incomplete or imprecise
   - Terminology or naming that has evolved
6. Explore the specified area in more depth than the initial pass
7. Create detailed documentation following the same methodology
8. Update existing docs with links to the new detailed docs
9. Ensure new docs link back to their parent high-level docs
10. **Record the new Git SHA** in all new/updated documents

### Time Expectations

This process should take hours, not minutes. A thorough expansion pass involves:
- Reading hundreds or thousands of lines of source code
- Tracing data flows through multiple files
- Verifying each architectural claim against actual implementation
- Running subagents in parallel to explore different aspects

If you're finishing in under an hour, you're probably not being thorough enough.

---

## Verification Agent Prompt

Use this when you want an independent agent — with no prior context — to deeply audit existing documentation
against the current codebase. This is not a spot-check; it's a thorough verification that everything documented
accurately reflects reality.

**When to Use This**

- After significant codebase changes (major refactors, new versions)
- Periodically (monthly/quarterly) to catch drift
- When onboarding to documentation created by others
- When you suspect docs may have become stale
- Before relying on docs for critical decisions

**Philosophy**

The verification agent operates as an auditor. It assumes nothing about the documentation's accuracy and
verifies every significant claim against actual code. This agent should:
- Start fresh with no assumptions
- Read source code directly, not rely on summaries
- Question whether each documented concept, flow, or architecture matches implementation
- Identify subtle inaccuracies that might mislead readers
- Spend hours being thorough — this is deep work

```
I need you to perform a deep verification audit of existing codebase documentation.

CONTEXT:
A previous AI agent explored a codebase and generated documentation following the Codebase Explorer
methodology. Your job is to verify that documentation is accurate — not as a cursory check, but as a
thorough audit that reads actual source code.

METHODOLOGY:
Please fetch the exploration methodology from:
https://raw.githubusercontent.com/[YOUR_USERNAME]/codebase-explorer/main/

Specifically, fetch:
- README.md (the methodology the original agent followed)
- LOADER.md (this file, for context on the verification process)
- All templates from /templates/ (to understand document structure)

WHAT TO VERIFY:
- Codebase location: [PATH_OR_URL]
- Existing documentation: [PATH_TO_DOCS_FOLDER]
- Area to verify: [SPECIFIC_AREA or "all"]

YOUR TASK:

1. Read the existing documentation completely
2. For EACH significant claim in the documentation:
   - Locate the relevant source code
   - Read and understand the actual implementation
   - Verify the claim is accurate and complete
   - Note any discrepancies, no matter how small

3. Specifically verify:
   - Architectural descriptions match actual code structure
   - Data flows described actually work that way
   - Component relationships are correctly documented
   - Internal terminology and names are current
   - Code examples (if any) are syntactically correct and functional
   - Cross-references between docs are valid

4. Check for drift patterns:
   - Code that evolved while docs stayed static
   - Features added that aren't documented
   - Features removed that are still documented
   - Subtle behavioral changes not reflected in docs

5. Produce a verification report:
   - What was verified and found accurate
   - What discrepancies were found (with specifics)
   - What documentation needs updating
   - What areas need deeper exploration

6. If authorized, fix the documentation directly

IMPORTANT:
- You have HOURS to complete this. Be thorough.
- Don't trust git diffs as your only signal — read the actual code
- Small inaccuracies matter; they compound into misleading documentation
- If something seems off, investigate deeply rather than assuming it's fine
- Use subagents to parallelize verification of independent areas
```

### Verification Checklist

The agent should verify each document type:

**Main Overview**
- [ ] Area categorization still makes sense
- [ ] All listed areas still exist and are correctly described
- [ ] Technology stack is current
- [ ] Architecture diagram (if any) matches reality

**Product Overviews**
- [ ] User stories reflect actual product capabilities
- [ ] Features listed are actually implemented
- [ ] Architecture descriptions match code
- [ ] "What's NOT covered here" sections are accurate

**Codebase Overviews**
- [ ] Directory structure matches actual structure
- [ ] Key files listed actually exist and do what's described
- [ ] Component interactions are correctly documented
- [ ] Internal terminology matches what's in code

**Glossary**
- [ ] All terms are still used in the codebase
- [ ] Definitions match actual usage
- [ ] No significant terms are missing
- [ ] Cross-references are valid

**Technology Mapping**
- [ ] Technologies listed are still in use
- [ ] Version numbers are current
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
| **Verifier** | AI Agent (Codebase Explorer methodology) |

## Summary

- **Documents verified**: [COUNT]
- **Accuracy rate**: [PERCENTAGE - claims verified as accurate]
- **Issues found**: [COUNT]
- **Severity**: [CRITICAL/MODERATE/MINOR]

## Verified as Accurate

[List major claims that were verified and found correct]

## Discrepancies Found

### [Issue 1 Title]
- **Document**: [path/to/doc.md]
- **Claim**: "[What the doc says]"
- **Reality**: "[What the code actually does]"
- **Severity**: [CRITICAL/MODERATE/MINOR]
- **Fix**: [What should change]

### [Issue 2 Title]
...

## Recommendations

[Overall recommendations for documentation maintenance]

## Files Examined

[List of source files that were read during verification]
```

---

## Alternative: No Network Access

If the AI agent can't fetch from GitHub, paste the README.md contents directly, then say:

```
I've pasted the methodology above. The templates are in the /templates folder of the same repo.
The methodology repo is at: [URL_TO_THIS_REPO]

Please proceed with exploring [CODEBASE_PATH] and save documentation to [OUTPUT_PATH].
```

The agent will ask you to paste templates as needed.

---

## What Generated Docs Should Include

When generating documentation, the agent should include references to this methodology so users know how to expand
and verify it later. Specifically, generated docs should:

1. **In the Main Overview's "Documentation Scope" section:**
   - Link to this LOADER.md file (the "Expanding Documentation Prompt" section)
   - Explain that users can start a new AI session with that prompt to drill deeper
   - Mention that verification agents can audit documentation accuracy

2. **In each area's "Documentation Scope" section:**
   - Note that this is high-level documentation
   - Point to LOADER.md for instructions on how to expand or verify docs

Example text for generated docs:
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
- **Parallel execution** (optional but faster, for exploring multiple areas simultaneously)
- **Fetch URLs** (optional, for loading templates from GitHub)
- **Web search** (optional, for looking up unfamiliar technologies and frameworks)

Most modern AI coding assistants (in IDEs or standalone) support these capabilities.
