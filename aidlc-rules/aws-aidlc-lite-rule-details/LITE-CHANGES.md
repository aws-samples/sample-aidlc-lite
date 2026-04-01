# AI-DLC Lite — Changes from Full Version

## Overview

AI-DLC Lite is a parallel version of the full AI-DLC configuration, designed for prototypes, demos, and simple projects. It preserves the same rules, structure, approval gates, audit logging, and state tracking, but surgically removes or modifies the parts that cause unnecessary depth — primarily mandatory follow-up question loops, redundant questioning categories, duplicate approval gates, and verbose rule repetition.

**Philosophy**: Get to working code faster without sacrificing correctness. Ask fewer questions but ask the right ones. One approval gate where the full version has two. Reasonable defaults over exhaustive clarification.

**What is NOT changed**: Approval gates (one per stage), audit.md logging, aidlc-state.md tracking, code location rules, brownfield file modification rules, artifact quality standards, and the three-phase lifecycle structure.

---

## Common Files

### Consolidated: 11 files → 2 files

| Original File | Lines | Disposition | Rationale |
|---|---|---|---|
| `process-overview.md` | 141 | Merged into `core-rules.md` §1 | Eliminated duplicate stage lists; replaced 77-line Mermaid diagram with compact ASCII |
| `terminology.md` | 190 | Merged into `core-rules.md` §2 | Removed duplicate stage lists (already in §1), verbose "When to Use" blocks, Planning vs Generation terminology |
| `welcome-message.md` | 110 | Merged into `core-rules.md` §3 | Removed duplicate ASCII diagram (already in §1), Phase Breakdown (repeats §1) |
| `depth-levels.md` | 74 | Merged into `core-rules.md` §4 | Removed worked examples (restate the principle without adding value) |
| `overconfidence-prevention.md` | 100 | Merged into `core-rules.md` §5 (MODIFIED) | Removed historical root-cause analysis, "Solution Implemented" section, maintenance section |
| `session-continuity.md` | 47 | Merged into `core-rules.md` §6 | Kept mostly intact — essential for workflow resumption |
| `workflow-changes.md` | 286 | Merged into `core-rules.md` §7 | Condensed each change type from full Scenario/Example/Handling/Considerations to Trigger/Steps/Key-risk format. Removed Logging Requirements and Best Practices (covered elsewhere) |
| `error-handling.md` | 374 | Merged into `core-rules.md` §8 | Phase-specific error handling tables condensed into general pattern + exceptions table. Removed verbose logging templates |
| `content-validation.md` | 79 | Merged into `core-rules.md` §9 | Merged with ASCII diagram standards |
| `ascii-diagram-standards.md` | 117 | Merged into `core-rules.md` §9 | Removed 4 of 5 ASCII pattern examples (kept Box Pattern only), removed redundant validation checklist |
| `question-format-guide.md` | 333 | Kept as separate `question-format-guide.md` (MODIFIED) | Stage files reference it; kept separate for modularity |

**Result**: 11 files (1,851 total lines) → 2 files (601 total lines) = **67% reduction**

### Modified Rules

| Rule | Full Version | Lite Version | Rationale |
|---|---|---|---|
| Questioning philosophy | "When in doubt, always ask" / "Default to Asking" | "Ask when ambiguity has high impact; prefer reasonable defaults for low-impact decisions" | Reduces unnecessary question rounds for clear requests |
| Follow-up questions | Mandatory unlimited loops until ALL ambiguities resolved | Max 1 follow-up round; if still unclear, note assumption and proceed | Prevents multi-round clarification cycles |
| Contradiction detection | Separate `{phase-name}-clarification-questions.md` files with multi-step workflow | Inline clarification in same question file (append Clarification section) | Eliminates extra file creation and round-trips |
| Overconfidence prevention | "No Proceeding with Ambiguity: Don't move forward until ALL ambiguities are resolved" | "Resolve Critical Ambiguity: Don't proceed when unclear on architecture, scope, or core requirements. For lower-impact details, state assumption and move forward." | Distinguishes high-impact from low-impact decisions |

---

## Inception Stage Files

### workspace-detection.md
- **Trimmed state file template**: Replaced verbose markdown code block in Step 4 with concise bullet-list description of required fields — Rationale: Template content is self-evident; the field list is sufficient
- **All 6 steps preserved**: No structural changes — Rationale: This stage is already lean and fully automated

### reverse-engineering.md
- **Consolidated 8 artifact files → 2**: `system-overview.md` (merges business-overview + architecture + code-structure + component-inventory + technology-stack) and `api-and-dependencies.md` (merges api-documentation + dependencies) — Rationale: 8 separate files is excessive for lite; same information preserved in 2 consolidated files
- **Dropped `code-quality-assessment.md`**: Not critical for prototypes — Rationale: Quality assessment adds time without changing implementation direction
- **Dropped `reverse-engineering-timestamp.md`**: Metadata tracked in aidlc-state.md — Rationale: Redundant with state tracking
- **Preserved**: Multi-package discovery (Step 1, all 6 sub-steps), approval gate, audit logging

### requirements-analysis.md
- **Step 5 (completeness analysis)**: Changed "MANDATORY: Evaluate ALL of these areas" → "Evaluate these areas, focusing on those most relevant to the request. For clear requests, a brief analysis suffices." — Rationale: For clear requests, exhaustive evaluation of all 6 areas adds no value
- **Step 6 (questions)**: Changed "ALWAYS create requirement-verification-questions.md unless requirements are exceptionally clear" → "Create questions only when the request has genuine ambiguity that would lead to wrong implementation direction. For clear, specific requests, proceed directly." — Rationale: The full version's mandate to always ask questions adds unnecessary rounds for clear requests
- **Removed mandatory unlimited follow-up loop**: Replaced with "ask up to 3 targeted follow-up questions in the same file. Then proceed." — Rationale: One round of follow-up is sufficient; assumptions can be documented
- **Preserved**: Steps 1-4 (context loading, analysis, depth, assessment), Steps 7-9 (requirements doc, state, approval), completion message format, audit logging

### user-stories.md
- **Collapsed two-part structure**: Removed separate PLANNING phase (Steps 1-14) and GENERATION phase (Steps 15-23) with two approval gates → Single 8-step flow with one approval gate — Rationale: The two-part plan-approve-generate-approve structure doubles interaction time
- **Removed `user-stories-assessment.md`**: Assessment done inline, not as separate artifact — Rationale: Separate assessment file adds overhead without value for lite
- **Removed `story-generation-plan.md`**: AI generates stories directly without requiring plan approval — Rationale: The user reviews the actual stories; plan approval is redundant
- **Removed separate plan approval gate**: Single approval after stories are generated — Rationale: One review achieves the same quality outcome faster
- **Reduced question categories**: Changed from 8 mandatory categories to "3-5 high-impact questions covering the most relevant categories" — Rationale: 8 mandatory categories is excessive when requirements already cover much of this
- **Removed mandatory follow-up loop (Step 10)**: Replaced with "up to 2 targeted follow-ups in same file" — Rationale: Prevents multi-round clarification cycles
- **Preserved**: Intelligent Assessment Guidelines (when to execute vs skip), output artifacts (stories.md, personas.md), INVEST criteria, single approval gate, audit logging

### workflow-planning.md
- **Trimmed Step 2 verbose sub-steps**: Condensed Related Component Identification and Cross-Package Impact into brief notes; condensed 4 layer impact sections into a single bulleted list; reduced Component Relationship Mapping from full template to brief paragraph — Rationale: The decision logic is essential; the verbose formatting is not
- **Simplified Step 6 Mermaid styling**: Brief style guidelines instead of listing every CSS rule — Rationale: Styling details are implementation concern, not workflow logic
- **Trimmed Step 7 execution plan template**: Concise description of contents instead of full template — Rationale: Template structure is self-evident from the content description
- **Preserved**: Steps 1-3 (context loading, scope analysis, phase determination), Step 5 (multi-module coordination), approval gate, audit logging

### application-design.md
- **Step 4 (questions)**: Changed from 5 category list with "generate questions where user input is needed" → "Ask only questions where the answer meaningfully changes the design. Skip categories where reasonable defaults exist." — Rationale: Component structure questions are often answerable from requirements context
- **Removed mandatory follow-up (Step 9)**: Replaced with "ask up to 2 targeted clarifications in the same plan document. Then proceed." — Rationale: Unlimited follow-up loops add time without proportional value
- **Preserved**: All 4 artifacts (components.md, component-methods.md, services.md, component-dependency.md), approval gate, audit logging

### units-generation.md
- **Collapsed two-part structure**: Removed separate PLANNING (Steps 1-11) / GENERATION (Steps 12-19) with two approval gates → Single 8-step flow with one approval gate — Rationale: Same as user-stories — collapsing saves a full interaction round
- **Removed `unit-of-work-plan.md`**: AI creates decomposition directly without requiring plan approval — Rationale: User reviews the actual unit artifacts; plan approval is redundant
- **Removed separate plan approval gate**: Single approval after units are generated — Rationale: One review achieves same outcome faster
- **Reduced question categories**: Changed from 6 mandatory to "2-4 questions on the most impactful topics" — Rationale: Fewer, targeted questions are more effective
- **Removed mandatory follow-up loop**: Replaced with "up to 2 follow-ups in same file" — Rationale: Prevents multi-round clarification cycles
- **Preserved**: Output artifacts (unit-of-work.md, unit-of-work-dependency.md, unit-of-work-story-map.md), approval gate, audit logging

---

## Construction Stage Files

### functional-design.md
- **Step 3 (questions)**: Changed from "evaluate ALL categories" across 7 categories with "When in doubt, ask the question" → "Ask 3-5 questions on the categories most relevant to this unit. Skip categories where the answer is evident from requirements/stories." — Rationale: 7 mandatory question categories is excessive when requirements and stories already cover much of this
- **Removed mandatory follow-up in Step 5**: Replaced with "ask up to 2 targeted clarifications, then proceed" — Rationale: One round of clarification is sufficient
- **Preserved**: 9-step structure, all 3 artifacts (business-logic-model.md, business-rules.md, domain-entities.md), approval gate, audit logging

### nfr-requirements.md
- **Step 3 (questions)**: Changed from 8 mandatory categories ("consider ALL categories") → "Ask 3-5 questions on the NFR categories most relevant to this project type. For prototypes/demos, focus on tech stack selection and skip detailed scalability/availability analysis." — Rationale: 8 NFR categories is thorough analysis; for prototypes, tech stack + basic performance is usually sufficient
- **Removed mandatory follow-up in Step 5**: Replaced with "ask up to 2 targeted clarifications" — Rationale: Prevents multi-round clarification cycles
- **Preserved**: 9-step structure, both artifacts (nfr-requirements.md, tech-stack-decisions.md), approval gate, audit logging

### nfr-design.md
- **Lightly trimmed**: Slightly condensed question categories directive wording — Rationale: Already the most lite-compatible construction file (uses "adapt as needed", "Skip entire categories if not applicable")
- **Preserved**: All 9 steps, both artifacts, approval gate, audit logging

### infrastructure-design.md
- **Lightly trimmed**: Slightly condensed question categories directive wording — Rationale: Already reasonably lean (uses selective questioning)
- **Preserved**: All 9 steps, all artifacts, approval gate, audit logging

### code-generation.md
- **Collapsed two-part structure**: Removed separate PART 1 (Planning, Steps 1-9 with plan approval) and PART 2 (Generation, Steps 10-16 with code approval) → Single 7-step flow with one approval gate — Rationale: Plan approval before code generation adds a full interaction round; the user reviews the actual code anyway
- **Removed `{unit-name}-code-generation-plan.md`**: AI still creates a plan internally but doesn't write it as a separate user-approved artifact — Rationale: The plan is a means to an end; the code is what matters
- **Removed plan approval gate**: Single approval after code is generated — Rationale: One review of actual code is more valuable than reviewing a plan then reviewing code
- **PRESERVED COMPLETELY**: Code Location Rules (application code at workspace root, never aidlc-docs/) and Brownfield File Modification Rules (check exists, modify in-place, never create copies, verify no duplicates) — Rationale: These are non-negotiable correctness rules
- **Preserved**: Story traceability, audit logging

### build-and-test.md
- **Consolidated 4-8 instruction files → 2**: `build-and-test-instructions.md` (merges build-instructions + unit-test-instructions + integration-test-instructions) and `build-and-test-summary.md` — Rationale: Separate instruction files per test type is overhead for prototypes
- **Conditional test files**: Performance, contract, security, and E2E test instruction files only generated when explicitly relevant to the project — Rationale: Prototypes rarely need all test types
- **Preserved**: Step 1 (analysis), state tracking, results presentation, audit logging

---

## Operations Stage Files

### operations.md
- **Copied as-is**: Already a placeholder — Rationale: No changes needed

---

## Steering Directory

### `steering/aws-aidlc-lite-rules/`
- Created as `steering/aws-aidlc-lite-rules/`, parallel to the full version's `steering/aws-aidlc-rules/`
- To be populated with steering rules that reference the lite rule details

---

## Summary Statistics

| Metric | Full Version | Lite Version | Reduction |
|---|---|---|---|
| Total files | 22 | 16 | 27% fewer files |
| Common files | 11 | 2 | 82% fewer |
| Total lines (common) | ~1,851 | ~601 | 67% reduction |
| Total lines (all) | ~4,500 | ~2,203 | 51% reduction |
| Approval gates per two-part stage | 2 | 1 | 50% fewer gates |
| Max follow-up question rounds | Unlimited | 1 | Bounded |
| Mandatory question categories | 5-8 per stage | 2-5 per stage | Targeted |
| Separate clarification files | Yes | No (inline) | Eliminated |
