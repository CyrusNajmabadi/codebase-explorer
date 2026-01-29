# Component Catalog Template

This template provides the structure for a quick-reference list of all major components in the codebase. Works for
services, libraries, assemblies, packages, or any major unit of organization.

---

## When to Use This Template

| Codebase Type       | "Component" Means    | Example                                    |
|---------------------|----------------------|--------------------------------------------|
| Microservices       | Services, APIs       | `auth-service`, `billing-api`              |
| Library/SDK         | Assemblies, packages | `Microsoft.CodeAnalysis.dll`, `@babel/parser` |
| Monolith            | Modules, subsystems  | `UserModule`, `PaymentSubsystem`           |
| Compiler/Toolchain  | Layers, phases       | `Parser`, `SemanticAnalyzer`, `CodeGen`    |

---

## Template Structure

```markdown
# [CODEBASE_NAME] Component Catalog

**Last Updated:** [DATE]

Quick reference for all major components in the codebase. For detailed architecture, see individual area documentation.

---

## How to Use This Catalog

- **Looking for a component?** Ctrl+F by name or description
- **Need details?** Click through to the component's documentation
- **New to the codebase?** Start with the [Main Overview](./[main_overview].md)

---

## Components by Area

### [AREA_1]

| Component       | Type                  | Purpose               | Code               | Docs              |
|-----------------|-----------------------|-----------------------|--------------------|-------------------|
| `[COMPONENT_1]` | [service/library/layer]| [One-line description]| [`[dir/]`]([link]) | [Overview]([link])|
| `[COMPONENT_2]` | [service/library/layer]| [One-line description]| [`[dir/]`]([link]) | [Overview]([link])|

### [AREA_2]

| Component       | Type   | Purpose               | Code               | Docs              |
|-----------------|--------|-----------------------|--------------------|-------------------|
| `[COMPONENT_3]` | [type] | [One-line description]| [`[dir/]`]([link]) | [Overview]([link])|

[Repeat for each area]

---

## Alphabetical Index

| Component       | Area   | Type   | Purpose    |
|-----------------|--------|--------|------------|
| `[COMPONENT_A]` | [AREA] | [type] | [One-line] |
| `[COMPONENT_B]` | [AREA] | [type] | [One-line] |
[Continue alphabetically]

---

## Dependency Graph

### Core Components (Many Depend On)

| Component  | Depended On By                  |
|------------|---------------------------------|
| `[CORE_1]` | [List of dependent components]  |
| `[CORE_2]` | [List of dependent components]  |

### Layer Diagram (for layered architectures)

```
┌─────────────────────────────────────────────┐
│            Application Layer                 │
│    [APP_COMPONENT_1]  [APP_COMPONENT_2]     │
└──────────────────┬──────────────────────────┘
                   │
┌──────────────────▼──────────────────────────┐
│            Core/Domain Layer                 │
│    [CORE_COMPONENT_1]  [CORE_COMPONENT_2]   │
└──────────────────┬──────────────────────────┘
                   │
┌──────────────────▼──────────────────────────┐
│          Infrastructure Layer                │
│    [INFRA_COMPONENT_1]  [INFRA_COMPONENT_2] │
└─────────────────────────────────────────────┘
```

### Service Diagram (for service-oriented architectures)

```
          ┌─────────────────┐
          │   [GATEWAY]     │
          └────────┬────────┘
                   │
    ┌──────────────┼──────────────┐
    ▼              ▼              ▼
┌───────┐      ┌───────┐      ┌───────┐
│ SVC_A │      │ SVC_B │      │ SVC_C │
└───────┘      └───────┘      └───────┘
```

---

## External Dependencies

| Component       | External Dependencies              |
|-----------------|------------------------------------|
| `[COMPONENT_1]` | [DATABASE], [API], [LIBRARY]       |
| `[COMPONENT_2]` | [FRAMEWORK], [CLOUD_SERVICE]       |

---

## Component Communication

### For Service-Oriented Codebases

| From      | To        | Protocol        | Purpose |
|-----------|-----------|-----------------|---------|
| `[SVC_A]` | `[SVC_B]` | gRPC/HTTP/Kafka | [Why]   |

### For Library-Oriented Codebases

| Consumer  | Dependency | Via                   | Purpose |
|-----------|------------|-----------------------|---------|
| `[LIB_A]` | `[LIB_B]`  | Direct reference      | [Why]   |
| `[LIB_B]` | `[LIB_C]`  | Interface/abstraction | [Why]   |

---

## Public vs Internal

[For library codebases, distinguish public API surface from internal implementation]

### Public API Components

| Component       | Public Surface             | Stability               |
|-----------------|----------------------------|-------------------------|
| `[COMPONENT_1]` | [Namespaces/types exposed] | [Stable/Preview/Internal]|

### Internal Components

| Component      | Purpose        | Why Internal     |
|----------------|----------------|------------------|
| `[INTERNAL_1]` | [What it does] | [Why not public] |

---

## Quick Reference Cards

### [IMPORTANT_COMPONENT_1]

```
Name:       [COMPONENT_NAME]
Type:       [service/library/layer/assembly]
Purpose:    [One-line]
Code:       [directory/]
Public API: [Yes/No/Partial]
Depends On: [LIST]
Used By:    [LIST]
Docs:       [LINK]
```

[Repeat for key components]
```

---

## Writing Tips

1. **Clarify what "component" means** in this codebase upfront

2. **Include the "Type" column** — Helps readers understand the architecture style

3. **Show both dependency directions** — "depends on" AND "used by"

4. **For libraries, note public vs internal** — Critical for understanding API surface

5. **Layer diagrams for layered architectures** — Visual hierarchy helps

6. **Keep descriptions to one line** — This is a lookup table

---

## Archetype-Specific Guidance

### For Service-Oriented Codebases
- Focus on service boundaries, protocols, health endpoints
- Include deployment information if relevant
- Note which services are critical path

### For Library/SDK Codebases
- Focus on public API surface
- Note assembly/package boundaries
- Include versioning/compatibility notes

### For Compiler/Toolchain Codebases
- Focus on pipeline stages
- Show data transformations between stages
- Note extension points
