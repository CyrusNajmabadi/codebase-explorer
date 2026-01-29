# Codebase Explorer - Loader Prompts

This file contains prompts to start AI agent sessions for codebase exploration. There are two main scenarios:
1. **Initial exploration** — First time exploring a codebase
2. **Expanding documentation** — Drilling deeper into an area that already has high-level docs

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
area.

```
I have a codebase with existing AI-generated documentation that I'd like to expand.

Please fetch the exploration methodology and templates from:
https://raw.githubusercontent.com/[YOUR_USERNAME]/codebase-explorer/main/

Specifically, fetch:
- README.md (the main methodology)
- LOADER.md (for reference)
- All templates from /templates/

Then:
1. Read the existing documentation at: [PATH_TO_DOCS_FOLDER]
2. Start with the Main Overview and Glossary to understand what's already documented
3. I'd like to drill deeper into: [SPECIFIC_AREA - e.g., "the parser component" or "authentication flow"]

Please create detailed documentation for that area, linking back to the existing high-level docs.
```

### What the Agent Should Do

1. Fetch and read the methodology (README.md) and templates
2. Read existing documentation to understand current state
3. Explore the specified area in more depth than the initial pass
4. Create detailed documentation following the same methodology
5. Update existing docs with links to the new detailed docs
6. Ensure new docs link back to their parent high-level docs

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
it later. Specifically, generated docs should:

1. **In the Main Overview's "Documentation Scope" section:**
   - Link to this LOADER.md file (the "Expanding Documentation Prompt" section)
   - Explain that users can start a new AI session with that prompt to drill deeper

2. **In each area's "Documentation Scope" section:**
   - Note that this is high-level documentation
   - Point to LOADER.md for instructions on how to request detailed docs

Example text for generated docs:
```markdown
## Documentation Scope

This documentation provides a high-level overview. To expand coverage of specific areas, start a new AI session
using the [Expanding Documentation Prompt](https://github.com/[USER]/codebase-explorer/blob/main/LOADER.md#expanding-documentation-prompt).
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
