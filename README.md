# Codebase Explorer: Deep-Dive Methodology for Complex Codebases

**Purpose:** A systematic approach for understanding large, unfamiliar codebases. Designed for experienced developers
who need to quickly build mental models of complex systems.

**Target Audience:** You (the AI agent) helping a developer explore a new codebase.

---

## Prerequisites

### Required Capabilities

This methodology assumes the AI agent can:
- **Read files** from the filesystem or repository
- **Search code** (grep, ripgrep, or similar)
- **Write files** to create documentation
- **List directories** to understand structure

### Optional (But Helpful) Capabilities

- **Parallel execution** — Explore multiple areas simultaneously (faster, not required)
- **Execute shell commands** — Useful for build system exploration
- **Fetch URLs** — Load templates from GitHub instead of pasting
- **Web search** — Look up unfamiliar technologies, frameworks, or patterns

### Adapting to Your AI's Capabilities

- **No parallelization?** Explore areas sequentially. Takes longer but works fine.
- **No shell access?** Skip build system command verification; focus on config files.
- **No URL fetching?** Paste templates directly when needed.

---

## Table of Contents

1. [Philosophy](#philosophy)
2. [Phase 1: Initial Assessment](#phase-1-initial-assessment)
3. [Phase 2: Deep Exploration](#phase-2-deep-exploration)
4. [Phase 3: Documentation](#phase-3-documentation)
5. [Phase 4: Verification](#phase-4-verification)
6. [Adaptation Guidelines](#adaptation-guidelines)
7. [Quality Standards](#quality-standards)

---

## Philosophy

### Core Principles

1. **Breadth before depth.** Understand the landscape before diving into details. A developer who knows "there are
   12 major areas and here's what each does" is more effective than one who deeply understands 1 area but is lost
   everywhere else.

2. **Progressive complexity.** Start accessible, go deep. Every document should be readable by someone unfamiliar
   with the codebase, then progressively reveal complexity.

3. **Stories over specifications.** "Why does this exist?" is more valuable than "What are all its methods?" Lead
   with realistic scenarios that show purpose, then provide technical details.

4. **Internal names matter.** Every codebase has jargon, codenames, and acronyms. Capturing these is critical—they're
   the vocabulary needed to read the code and communicate with the team.

5. **Architecture over implementation.** Focus on how components interact, what design patterns are used, and why
   decisions were made. Line-by-line code details are less valuable than understanding the shape of the system.

6. **Verify, don't hallucinate.** When uncertain, say so. When making inferences, label them. Better to leave gaps
   than fill them with plausible-sounding fiction.

7. **Look things up.** When you encounter unfamiliar technologies, frameworks, or patterns, search the web to
   understand them rather than guessing. This ensures accurate documentation and helps you recognize how standard
   tools are being used (or customized) in this codebase.

8. **Find and reference existing docs.** Before writing, check for existing documentation in the codebase (README
   files, doc/ folders, wikis, inline comments). Reference and link to these rather than duplicating. Your docs
   should complement what exists, not replace it.

9. **Track version information.** If the codebase is a git repository, record the commit SHA when generating docs.
   This enables incremental updates—when revisiting docs, you can diff what changed since the last documentation
   pass and focus updates on modified areas.

### Tone and Style

Documentation should be **clear, professional, and factual**. Avoid language that feels like marketing copy or
AI-generated fluff.

**Do:**
- State facts directly: "The parser converts source text to syntax trees."
- Use neutral language: "This approach has trade-offs..." 
- Be specific: "Processes approximately 10,000 files" not "handles massive scale"
- Acknowledge limitations: "This overview covers the main components; see [link] for details."

**Don't:**
- Use emotional language: "painful", "exciting", "revolutionary", "game-changing"
- Exaggerate: "blazingly fast", "incredibly powerful", "seamless"
- Use filler phrases: "It's worth noting that...", "Interestingly enough..."
- Be dramatic: "When disaster strikes...", "The moment of truth..."
- Use second-person dramatically: "You're frantically searching..." (factual "you" is fine)

**Examples:**

| Instead of | Write |
|------------|-------|
| "This solves the painful problem of..." | "This addresses the problem of..." |
| "The elegant solution handles..." | "The solution handles..." |
| "You'll love how it seamlessly..." | "It integrates with..." |
| "The incredibly powerful engine..." | "The engine supports..." |
| "When things go wrong, chaos ensues" | "When errors occur, the system..." |

### Diagrams

ASCII diagrams are useful but difficult to align correctly. Keep them simple:

- Use basic box characters: `┌ ┐ └ ┘ │ ─ ├ ┤ ┬ ┴ ┼`
- Prefer simple arrows: `→ ← ↓ ↑ ▶ ▼`
- Keep boxes short (avoid long text that causes alignment issues)
- When in doubt, use a simpler diagram or describe the flow in text
- If a diagram looks misaligned, simplify it rather than trying to fix alignment

Simple and correct is better than complex and broken.

---

## Phase 1: Initial Assessment

**Goal:** Understand the shape of the codebase before exploring deeply.

### Step 1.1: Structural Survey

Start by understanding the physical layout:

```
Questions to answer:
- How many top-level directories exist?
- Is this a monorepo or multi-repo?
- What languages are present? (check file extensions, build files)
- What build system(s) are used? (Bazel, Maven, npm, Cargo, etc.)
- Are there obvious groupings? (services/, libs/, apps/, etc.)
```

**Actions:**
- List top-level directories
- Check for build files (BUILD, pom.xml, package.json, Cargo.toml, etc.)
- Look for README files, CLAUDE.md, AGENTS.md, or similar documentation
- Check for a docs/ folder or wiki

### Step 1.2: Scale Assessment

Determine the codebase's complexity:

| Scale   | Top-Level Dirs | Likely Approach                                  |
|---------|----------------|--------------------------------------------------|
| Small   | < 10           | Explore each directly                            |
| Medium  | 10-50          | Group into 5-10 themes                           |
| Large   | 50-200         | Group into 10-15 areas, use parallel exploration |
| Massive | 200+           | Hierarchical grouping, heavy parallelization     |

### Step 1.3: Ask Clarifying Questions

Before deep exploration, ask the user:

1. **Context:** "What is this codebase for? What does the product/company do?"
2. **Focus areas:** "Are there specific areas you care most about?"
3. **Your role:** "What will you be working on? (e.g., backend, ML, infra)"
4. **Known trouble spots:** "Are there areas that are particularly confusing or poorly documented?"
5. **Output location:** "Where should I save the documentation?"

If the user can't answer these, that's fine—proceed with exploration and infer what you can.

---

## Phase 2: Deep Exploration

**Goal:** Build comprehensive understanding through parallel, systematic exploration.

### Step 2.1: Define Exploration Areas

Based on the initial assessment, group the codebase into 8-15 logical areas. These might be:

- By product (auth, billing, analytics, ML)
- By layer (frontend, backend, infrastructure)
- By domain (users, content, payments)
- By a combination

**Good area definitions:**
- Clear boundaries
- Roughly similar scope
- Map to how developers think about the system

### Step 2.2: Parallel Deep Exploration

For each area, launch a parallel exploration task (or explore sequentially if parallelization isn't available):

```
Explore the [AREA_NAME] area of this codebase.

Focus on:
1. What services/components exist?
2. What is the architecture? (draw a mental picture)
3. What technologies are used?
4. What design patterns appear?
5. What are the internal names/jargon?
6. How does this area interact with other areas?
7. What would a new developer find confusing?

Be VERY THOROUGH. Check multiple directories, read key files, understand the structure.

Return:
- Key findings (bullet points)
- Architecture summary
- Technology choices
- Internal terminology
- Open questions
```

**Parallelization guidance:**
- Run 3-4 parallel explorations at a time (more may cause resource contention)
- Wait for results before launching next batch
- Collect all findings before writing documentation
- If parallelization isn't available, explore areas sequentially—it takes longer but works fine

**When to search the web:**
- You encounter a framework, library, or tool you're unfamiliar with
- You see patterns or conventions that might be standard practices for a technology
- You need to verify how a technology is typically used vs. how it's used here
- You want to link to official documentation for external technologies

### Step 2.3: Synthesis

After all explorations complete:

1. **Identify themes:** What patterns appear across areas?
2. **Map dependencies:** Which areas interact with which?
3. **Collect terminology:** Build a unified glossary
4. **Note gaps:** What couldn't you figure out?

---

## Phase 3: Documentation

**Goal:** Produce clear, useful documentation that helps developers navigate the codebase.

### Document Types

Generate these documents using the templates in the `/templates` folder:

| Document                        | Purpose                                  | When to Create       |
|---------------------------------|------------------------------------------|----------------------|
| **Main Overview**               | Entry point, map of everything           | Always               |
| **Glossary**                    | Internal names, acronyms, jargon         | Always               |
| **Technology Mapping**          | What tech is used where                  | Always               |
| **Product Overview**            | Why an area matters (with story)         | Per major area       |
| **Codebase Overview**           | How an area works (architecture)         | Per major area       |
| **Build System Overview**       | How code is built                        | If complex           |
| **Test Infrastructure Overview**| How code is tested                       | If complex           |
| **Component Catalog**           | Quick reference for all components       | If 20+ components    |
| **Request Flow**                | Trace a request through the system       | Optional, high value |

### Document Creation Order

1. **Glossary first** — You'll reference it everywhere
2. **Main Overview** — Creates the map
3. **Product Overviews** — Establish the "why"
4. **Codebase Overviews** — Explain the "how"
5. **Specialized docs** — Build system, testing, etc.
6. **Technology Mapping** — Synthesize across areas

### Writing Guidelines

**For Product Overviews:**
- Lead with a story (see template)
- Explain why this area exists and what problem it solves
- Assume the reader is smart but unfamiliar
- Save technical details for the codebase overview

**For Codebase Overviews:**
- Start with an architecture diagram (ASCII or Mermaid)
- List key components in tables
- Explain design patterns and why they're used
- Include internal names and link to glossary
- Add "Important Links" for external technologies

**For All Documents:**
- Use progressive complexity (accessible intro → deep details)
- Cross-reference other documents
- Include "Last Updated" dates
- End with links to related docs

---

## Phase 4: Verification

**Goal:** Ensure documentation is accurate and doesn't contain hallucinations.

### Verification Checklist

1. **Fact-check specific claims:**
   - File counts, directory names
   - Technology versions
   - Component/service names and purposes

2. **Verify code references:**
   - Do referenced files/functions exist?
   - Are paths correct?

3. **Check internal consistency:**
   - Do glossary terms match usage in documents?
   - Do cross-references work?

4. **Flag uncertainties:**
   - Mark inferences with "appears to" or "likely"
   - Note areas where exploration was limited

### Verification Report

Create a brief report noting:
- What was verified
- What couldn't be verified
- Known limitations
- Suggested follow-ups for the user

---

## Adaptation Guidelines

Not all codebases are the same. Here's how to adapt:

### Codebase Archetypes

Different codebase types have different organizational patterns. Adapt terminology accordingly:

| Archetype              | "Component" Means              | "Flow" Means                         | Example Codebases           |
|------------------------|--------------------------------|--------------------------------------|-----------------------------|
| **Service-Oriented**   | Services, APIs, microservices  | HTTP/RPC request through services    | Kubernetes, Databricks      |
| **Library/SDK**        | Assemblies, packages, modules  | API call through layers              | Roslyn, React, NumPy        |
| **Compiler/Toolchain** | Pipeline stages, passes        | Source → IR → Output                 | LLVM, GCC, Babel            |
| **Monolithic App**     | Modules, subsystems            | User action → handler → DB           | WordPress, Rails apps       |
| **Data Platform**      | Pipelines, jobs, transforms    | Data ingestion → processing → output | Airflow, dbt, Spark         |

**For Service-Oriented Codebases:**
- Focus on service boundaries, protocols, deployment
- Document inter-service communication patterns
- Include health endpoints, scaling behavior
- "Request flow" = HTTP/gRPC through services

**For Library/SDK Codebases:**
- Focus on public API surface vs internal implementation
- Document layer dependencies and abstractions
- Include extension points, plugin systems
- "Flow" = API call through abstraction layers

**For Compiler/Toolchain Codebases:**
- Focus on pipeline stages and data transformations
- Document intermediate representations
- Include optimization passes, error handling
- "Flow" = source → parse → analyze → transform → emit

### For Smaller Codebases (< 20 top-level dirs)

- May not need parallel exploration—explore directly
- Fewer areas, deeper coverage per area
- Might combine product + codebase overviews
- Skip component catalog if < 10 major components

### For Deeply Nested Codebases

- Focus on the nesting structure itself
- May need multiple levels of overview docs
- Use the directory structure as your guide

### For Multi-Repo Setups

- Create a "meta" overview that maps repos
- Each repo might get its own documentation set
- Focus on cross-repo interactions

### For Specific Domains

**ML/AI codebases:**
- Add model registry, training pipeline, serving infrastructure sections
- Focus on experiment tracking, feature stores

**Frontend codebases:**
- Add component library, state management sections
- Focus on build tooling, testing patterns

**Infrastructure codebases:**
- Add deployment pipeline, cloud resource sections
- Focus on IaC patterns, monitoring

### When Existing Docs Exist

- Read them first
- Note gaps and outdated sections
- Augment rather than replace
- Reference existing docs where appropriate

---

## Incremental Documentation Workflow

Documentation doesn't need to be completed in one session. The recommended approach is iterative:

### Phase 1: Initial High-Level Pass

Create the foundation:
- Main Overview (map of everything)
- Glossary (terms you encounter)
- Product Overviews for major areas (why they exist)
- High-level Codebase Overviews (architecture, not implementation details)

**Record version information:** If this is a git repository, record the current commit SHA. Include this in each
generated document's metadata section (see templates). This enables incremental updates later.

**Leave expansion points:** When you identify areas that deserve more detail, note them explicitly:
- "For detailed compilation flow, see [Compilation Flow](./flows/compilation.md)" (even if that doc doesn't exist yet)
- Include a "## Areas for Future Documentation" section listing what could be expanded

### Phase 2+: Expand on Demand

When a user returns (same session or new session) and asks to drill into an area:

1. **Read existing documentation first** — Understand what's already documented
2. **Identify the expansion point** — What specific area needs more detail?
3. **Create detailed docs that link back** — New docs should reference the high-level docs they expand on
4. **Update the parent docs** — Add links from high-level docs to the new detailed docs

### Handling "Expand This Area" Requests

When asked to go deeper on an area with existing high-level docs:

```
User: "I need to understand the auth system in more detail"

Agent should:
1. Read existing auth-related docs (product overview, codebase overview)
2. Explore the auth code more deeply than the initial pass
3. Create:
   - Detailed component docs for auth subsystems
   - Flow docs for key auth operations (login, token refresh, etc.)
   - Expanded glossary entries for auth-specific terms
4. Update existing docs to link to new detailed docs
```

### Marking Documentation as Incomplete

High-level documentation should clearly state its scope and limitations. Include a notice like:

```markdown
---

**Documentation Scope:** This document provides a high-level overview of [AREA]. It covers architecture and major
components but does not detail internal implementation. For deeper exploration of specific components, see the
[Incremental Documentation Guide](./README.md#expanding-documentation) or ask the AI agent to drill into a
specific area.

---
```

### Linking Between Levels

**High-level docs should:**
- State explicitly what they cover and what they don't
- Link to detailed docs where they exist
- Note areas that could be expanded (even without existing docs)
- Reference the methodology for how to request deeper documentation

**Detailed/drill-in docs should:**
- Link back to their parent high-level doc: "This expands on the Parser section of [Compiler Overview](../compiler_overview.md)"
- State their scope: "This document covers the Lexer component in detail"
- Link to sibling docs at the same level: "See also: [Binder Details](./binder.md), [Checker Details](./checker.md)"

**Cross-reference pattern:**
```
Main Overview
    ↓ links to
Area Product Overview ← "For high-level context, see Main Overview"
    ↓ links to
Area Codebase Overview ← "Part of [Area] documentation"
    ↓ links to (when created)
Component Detail Doc ← "This expands on [Section] from Codebase Overview"
    ↓ links to (when created)
Flow Doc ← "This details [Operation] within [Component]"
```

### Starting a "Drill Deeper" Session

Users should start a drill-in session using the **Expanding Documentation Prompt** from `LOADER.md`. This ensures
the agent loads the methodology and templates before expanding existing docs.

When you (the agent) receive such a request:

1. **Fetch the methodology** — Load README.md and templates from the methodology repo
2. **Read the existing Main Overview** — Understand the current documentation structure and note the git SHA
3. **Check what changed (if git repo):**
   - Get the current git SHA: `git rev-parse HEAD`
   - Compare to the SHA recorded in existing docs
   - If different, check what changed: `git diff --stat OLD_SHA..HEAD -- path/to/area/`
   - Focus documentation updates on modified files/areas
4. **Check what exists** — List the documentation directory to see what's documented
5. **Read relevant existing docs** — Before exploring code, understand what's already captured
6. **Ask clarifying questions if needed** — "Which specific aspect of [AREA] would you like me to detail?"
7. **Explore and expand** — Go deeper on the requested area, prioritizing changed code if updating
8. **Maintain consistency** — Use the same terminology, structure, and style as existing docs
9. **Update links** — Add links from parent docs to new detailed docs, and vice versa
10. **Update version metadata** — Record the new git SHA in updated/new docs

### What Generated Docs Must Include

Generated documentation should be **self-documenting** about how to expand it. Every generated doc should include:

1. **Methodology reference** — Link to the GitHub repo containing this methodology
2. **LOADER.md reference** — Link specifically to LOADER.md#expanding-documentation-prompt
3. **Scope statement** — What this doc covers and what it doesn't
4. **Parent/child links** — Links up to parent docs and down to detailed docs (where they exist)

The templates include `[METHODOLOGY_URL]` placeholders. When generating docs, replace these with the actual URL
to the methodology repo (provided by the user in the initial prompt).

This ensures that anyone reading the generated docs knows:
- That this is AI-generated documentation following a specific methodology
- How to request more detailed documentation
- What prompt to use to start a drill-in session

---

## Quality Standards

### Document Length Guidelines

| Document Type        | Target Length |
|----------------------|---------------|
| Main Overview        | 800-1200 lines|
| Product Overview     | 200-300 lines |
| Codebase Overview    | 250-400 lines |
| Glossary             | Varies        |
| Technology Mapping   | 150-250 lines |
| Specialized Overviews| 400-800 lines |

### Must-Have Elements

Every documentation set should include:

- [ ] Clear entry point (main overview)
- [ ] Glossary of internal terms
- [ ] Architecture diagrams for major areas
- [ ] Stories/narratives for product context
- [ ] Cross-references between documents
- [ ] "Last Updated" dates
- [ ] Links to external technology documentation

### Avoid

- Hallucinating file paths or component names
- Over-confident claims about code you haven't read
- Excessive length without proportional value
- Jargon without definition
- Orphan documents with no cross-references

---

## Quick Start

When a user asks you to explore a codebase:

1. **Fetch methodology files** — README.md, LOADER.md, and all templates from `/templates`
2. **Note the methodology URL** — The user should provide this; you'll include it in generated docs so users know
   how to expand documentation later
3. **Run initial assessment** (Phase 1)
4. **Ask clarifying questions** if needed
5. **Launch parallel exploration** (Phase 2)
6. **Synthesize and document** (Phase 3) — Replace `[METHODOLOGY_URL]` placeholders with the actual URL
7. **Verify** (Phase 4)
8. **Deliver** with a summary of what you created and how to expand it

---

## Templates

The following templates are available in the `/templates` folder:

- `main_overview.md` — Entry point document
- `product_overview.md` — Per-area product context with story
- `codebase_overview.md` — Per-area technical architecture
- `glossary.md` — Internal terminology
- `technology_mapping.md` — Tech usage across the codebase
- `build_system_overview.md` — Build infrastructure
- `test_infrastructure_overview.md` — Testing infrastructure
- `component_catalog.md` — Quick-reference component list
- `request_flow.md` — End-to-end request/data tracing

Fetch and read these templates before generating documentation.
