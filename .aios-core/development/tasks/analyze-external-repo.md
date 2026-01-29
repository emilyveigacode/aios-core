---
id: analyze-external-repo
title: Analyze External Repository for AXIS Evolution
category: research
agent: aios-master
elicit: true
dependencies:
  - templates/repo-analysis-tmpl.yaml
output: docs/research/external-repos/{repo-name}_analysis.md
---

# Analyze External Repository

**Purpose**: Systematic analysis of external repositories to identify learnings, stack overlaps, and strategic opportunities for AXIS evolution.

**When to use**: When discovering a framework, library, or system that might inform AXIS architecture or capabilities.

---

## Process

### Phase 1: Repository Discovery & Context

**Agent prompt**:
```
I'm going to analyze an external repository to extract learnings for AXIS.

Please provide:
1. Repository URL (required)
2. Why this repo is interesting (1-2 sentences)
3. Specific areas of interest (optional: architecture, features, governance, etc.)
```

**Elicitation**:
- repo_url: string (required)
- interest_reason: text (required)
- focus_areas: list[string] (optional)

---

### Phase 2: Initial Reconnaissance

**Steps**:
1. Read repository README and main documentation
2. Identify core purpose and value proposition
3. Map primary technology stack
4. Extract key features and capabilities

**Output**: Structured context summary

---

### Phase 3: Stack Mapping

**Framework**:
```yaml
dimensions:
  - architecture: How is the system structured?
  - orchestration: How does it coordinate components?
  - data_model: How does it store and manage state?
  - governance: What rules and constraints exist?
  - observability: How is execution tracked?
  - extensibility: How can it be customized?
```

**For each dimension**:
- Document external repo approach
- Document AXIS current approach
- Identify: ✅ Overlap | ❌ Gap | 🎯 Differential

---

### Phase 4: Strategic Analysis

**Questions**:
1. **Validation**: Does this repo validate AXIS design choices?
2. **Gaps**: What does this repo do that AXIS doesn't?
3. **Differentials**: What does AXIS do better?
4. **Adoption Risk**: What would happen if we adopted this as dependency?

**Decision Matrix**:
```yaml
adopt_as_dependency:
  - Compatible with AXIS sovereignty? (Y/N)
  - Adds capabilities we can't build? (Y/N)
  - Maintained and stable? (Y/N)
  - Licensing compatible? (Y/N)

learn_and_diverge:
  - Specific concepts to extract
  - How to implement in AXIS context
  - Timeline (Q1/Q2/Long-term)

watch_and_monitor:
  - What metrics to track?
  - When to revisit?
```

---

### Phase 5: Action Planning

**Deliverables**:
1. **Comparison Document** (using template)
2. **Recommended Actions** (short/medium/long term)
3. **Strategic Decision** (Adopt / Learn / Watch / Dismiss)

**Template Location**: `.aios-core/development/templates/repo-analysis-tmpl.yaml`

---

## Execution

**Command**: `*analyze-repo` (from aios-master)

**Workflow**:
```bash
# Agent loads this task
# Elicits repo URL and context
# Executes phases 1-5
# Generates artifact in docs/research/external-repos/
# Adds entry to EXTERNAL_REPOS_REGISTRY.md
```

---

## Example Output Structure

```markdown
# Analysis: {repo-name} vs AXIS
**Date**: YYYY-MM-DD
**Analyst**: Orion (AIOS Master)

## Executive Summary
[Verdict table with key dimensions]

## Stack Mapping
[Detailed comparison per dimension]

## Strategic Analysis
[Adoption decision matrix results]

## Recommended Actions
[Short/Medium/Long term roadmap]

## References
[Links to repo, docs, related AXIS components]
```

---

## Quality Checklist

- [ ] Repository URL and context documented
- [ ] All 6 dimensions analyzed (architecture, orchestration, data, governance, observability, extensibility)
- [ ] Overlaps, gaps, and differentials identified
- [ ] Adoption decision matrix completed
- [ ] Recommended actions with timeline
- [ ] Document saved to `docs/research/external-repos/`
- [ ] Registry updated

---

## Notes

- This task is **research-focused**, not implementation
- Output should inform decision-making, not execute changes
- Keep analysis objective and strategic
- Focus on **learnings**, not NIH syndrome
