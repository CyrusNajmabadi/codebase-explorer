# Codebase Explorer - Loader Prompt

Copy and paste the text below into a new AI agent session to begin exploring a codebase.

---

## Loader Prompt (copy everything below this line)

```
I need your help understanding a complex codebase I'm unfamiliar with.

First, please fetch the exploration methodology from:
https://raw.githubusercontent.com/[YOUR_USERNAME]/codebase-explorer/main/README.md

Then fetch all templates from the /templates folder:
- main_overview.md
- product_overview.md  
- codebase_overview.md
- glossary.md
- technology_mapping.md
- build_system_overview.md
- test_infrastructure_overview.md
- component_catalog.md
- request_flow.md

Once you've loaded the methodology and templates, let's begin exploring:

Codebase location: [PATH_OR_URL]
Output location: [WHERE_TO_SAVE_DOCS]

Any specific areas I care about: [OPTIONAL - e.g., "backend services" or "the ML pipeline"]
```

---

## Usage Notes

1. Replace `[YOUR_USERNAME]` with your GitHub username (or org name)
2. Replace `[PATH_OR_URL]` with the codebase path (local) or repo URL
3. Replace `[WHERE_TO_SAVE_DOCS]` with where you want documentation saved
4. The "specific areas" field is optional but helps prioritize

## Alternative: No Network Access

If the AI agent can't fetch from GitHub, paste the README.md contents directly, then say:

```
I've pasted the methodology above. The templates are in the /templates folder of the same repo.
Please proceed with exploring [CODEBASE_PATH] and save documentation to [OUTPUT_PATH].
```

The AI agent will ask you to paste templates as needed, or will adapt the standard templates from the methodology.

---

## Required AI Capabilities

This methodology works best with AI agents that can:
- **Read files** from the local filesystem or repository
- **Search/grep** through code
- **Write files** to create documentation
- **Execute commands** (optional, for build system exploration)
- **Parallel execution** (optional but faster, for exploring multiple areas simultaneously)
- **Fetch URLs** (optional, for loading templates from GitHub)

Most modern AI coding assistants (in IDEs or standalone) support these capabilities.
