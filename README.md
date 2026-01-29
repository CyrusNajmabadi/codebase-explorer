# Codebase Explorer: Deep-Dive Methodology for Complex Codebases

**Purpose:** A systematic approach for understanding large, unfamiliar codebases. Designed for experienced developers who need to quickly build mental models of complex systems.

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

1. **Breadth before depth.** Understand the landscape before diving into details. A developer who knows "there are 12 major areas and here's what each does" is more effective than one who deeply understands 1 area but is lost everywhere else.

2. **Progressive complexity.** Start accessible, go deep. Every document should be readable by someone unfamiliar with the codebase, then progressively reveal complexity.

3. **Stories over specifications.** "Why does this exist?" is more valuable than "What are all its methods?" Lead with realistic scenarios that show purpose, then provide technical details.

4. **Internal names matter.** Every codebase has jargon, codenames, and acronyms. Capturing these is critical—they're the vocabulary needed to read the code and communicate with the team.

5. **Architecture over implementation.** Focus on how components interact, what design patterns are used, and why decisions were made. Line-by-line code details are less valuable than understanding the shape of the system.

6. **Verify, don't hallucinate.** When uncertain, say so. When making inferences, label them. Better to leave gaps than fill them with plausible-sounding fiction.

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

| Scale | Top-Level Dirs | Likely Approach |
|-------|----------------|-----------------|
| Small | < 10 | Explore each directly |
| Medium | 10-50 | Group into 5-10 themes |
| Large | 50-200 | Group into 10-15 areas, use parallel exploration |
| Massive | 200+ | Hierarchical grouping, heavy parallelization |

### Step 1.3: Ask Clarifying Questions

Before deep exploration, ask the user:

1. **Context:** "What is this codebase for? What does the product/company do?"
2. **Focus areas:** "Are there specific areas you care most about?"
3. **Your role:** "What will you be working on? (e.g., backend, ML, infra)"
4. **Known pain points:** "Are there areas that are particularly confusing or poorly documented?"
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

| Document | Purpose | When to Create |
|----------|---------|----------------|
| **Main Overview** | Entry point, map of everything | Always |
| **Glossary** | Internal names, acronyms, jargon | Always |
| **Technology Mapping** | What tech is used where | Always |
| **Product Overview** | Why an area matters (with story) | Per major area |
| **Codebase Overview** | How an area works (architecture) | Per major area |
| **Build System Overview** | How code is built | If complex |
| **Test Infrastructure Overview** | How code is tested | If complex |
| **Component Catalog** | Quick reference for all components | If 20+ components |
| **Request Flow** | Trace a request through the system | Optional, high value |

### Document Creation Order

1. **Glossary first** - You'll reference it everywhere
2. **Main Overview** - Creates the map
3. **Product Overviews** - Establish the "why"
4. **Codebase Overviews** - Explain the "how"
5. **Specialized docs** - Build system, testing, etc.
6. **Technology Mapping** - Synthesize across areas

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

| Archetype | "Component" Means | "Flow" Means | Example Codebases |
|-----------|-------------------|--------------|-------------------|
| **Service-Oriented** | Services, APIs, microservices | HTTP/RPC request through services | Kubernetes, Databricks, Stripe |
| **Library/SDK** | Assemblies, packages, modules | API call through layers | Roslyn, React, NumPy |
| **Compiler/Toolchain** | Pipeline stages, passes | Source → IR → Output | LLVM, GCC, Babel |
| **Monolithic App** | Modules, subsystems | User action → handler → DB | WordPress, Rails apps |
| **Data Platform** | Pipelines, jobs, transforms | Data ingestion → processing → output | Airflow, dbt, Spark |

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

## Quality Standards

### Document Length Guidelines

| Document Type | Target Length |
|---------------|---------------|
| Main Overview | 800-1200 lines |
| Product Overview | 200-300 lines |
| Codebase Overview | 250-400 lines |
| Glossary | Varies (comprehensive) |
| Technology Mapping | 150-250 lines |
| Specialized Overviews | 400-800 lines |

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

1. **Fetch templates** from this repo's `/templates` folder
2. **Run initial assessment** (Phase 1)
3. **Ask clarifying questions** if needed
4. **Launch parallel exploration** (Phase 2)
5. **Synthesize and document** (Phase 3)
6. **Verify** (Phase 4)
7. **Deliver** with a summary of what you created

---

## Templates

The following templates are available in the `/templates` folder:

- `main_overview.md` - Entry point document
- `product_overview.md` - Per-area product context with story
- `codebase_overview.md` - Per-area technical architecture
- `glossary.md` - Internal terminology
- `technology_mapping.md` - Tech usage across the codebase
- `build_system_overview.md` - Build infrastructure
- `test_infrastructure_overview.md` - Testing infrastructure
- `component_catalog.md` - Quick-reference component list
- `request_flow.md` - End-to-end request tracing

Fetch and read these templates before generating documentation.
