# Units Generation

## Overview
This stage decomposes the system into manageable units of work.

**DEFINITION**: A unit of work is a logical grouping of stories for development purposes. For microservices, each unit becomes an independently deployable service. For monoliths, the single unit represents the entire application with logical modules.

**Terminology**: Use "Service" for independently deployable components, "Module" for logical groupings within a service, "Unit of Work" for planning context.

## Prerequisites
- Context Assessment must be complete
- Requirements Assessment recommended (provides functional scope)
- Story Development recommended (stories map to units)
- Application Design phase REQUIRED (determines components, methods, and services)
- Execution plan must indicate Design phase should execute

---

## Step 1: Load Context

- Read `aidlc-docs/inception/requirements/requirements.md`
- Read `aidlc-docs/inception/user-stories/stories.md` (if available)
- Read `aidlc-docs/inception/application-design/components.md`
- Read `aidlc-docs/inception/application-design/component-methods.md`
- Read `aidlc-docs/inception/application-design/services.md`
- Read `aidlc-docs/inception/application-design/component-dependency.md`
- Load reverse engineering artifacts if brownfield

## Step 2: Generate Questions (If Needed)

Ask 2-4 questions on the most impactful topics. Consider: story grouping, unit dependencies, deployment model, and domain boundaries.

- Create `aidlc-docs/inception/application-design/units-questions.md` with questions using [Answer]: tag format
- Wait for user to provide answers
- If critical ambiguity remains, ask up to 2 follow-ups in the same file. Then proceed.

For projects where the application design already makes unit boundaries clear, this step may be skipped entirely.

## Step 3: Create Unit Decomposition

- Define units with clear responsibilities and boundaries
- Map stories to units (ensure every story is assigned)
- Document dependencies between units
- For greenfield: document code organization strategy (see code-generation.md for structure patterns)
- Validate unit boundaries: each unit should be independently developable and testable

## Step 4: Generate Unit Artifacts

- Create `aidlc-docs/inception/application-design/unit-of-work.md` with:
  - Unit name, purpose, and responsibilities
  - Components and modules contained in each unit
  - Greenfield: code organization strategy and directory structure
- Create `aidlc-docs/inception/application-design/unit-of-work-dependency.md` with:
  - Dependency matrix between units
  - Integration points and contracts
  - Build and deployment order constraints
- Create `aidlc-docs/inception/application-design/unit-of-work-story-map.md` with:
  - Stories assigned to each unit
  - Coverage verification (all stories mapped)
  - Priority ordering within each unit

## Step 5: Update State Tracking

Update `aidlc-docs/aidlc-state.md`:

```markdown
## Stage Progress
### INCEPTION PHASE
- [x] Workspace Detection
- [x] Reverse Engineering (if applicable)
- [x] Requirements Analysis
- [x] User Stories (if applicable)
- [x] Workflow Planning
- [x] Application Design
- [x] Units Generation
```

## Step 6: Present Completion Message

```markdown
# Units Generation Complete

[AI-generated summary of units and decomposition created in bullet points]

> **REVIEW REQUIRED:**
> Please examine the units generation artifacts at: `aidlc-docs/inception/application-design/`

> **WHAT'S NEXT?**
>
> **You may:**
>
> **Request Changes** - Ask for modifications to the units generation if required
> **Approve & Continue** - Approve units and proceed to **CONSTRUCTION PHASE**
```

## Step 7: Wait for Explicit Approval

- Do not proceed until the user explicitly approves the units generation
- Approval must be clear and unambiguous
- If user requests changes, update the units and repeat the approval process

## Step 8: Record Approval and Update Progress

- Log the user's approval response with timestamp in `aidlc-docs/audit.md`
- Include the exact user response text
- Mark the approval status clearly
- Mark Units Generation stage complete in `aidlc-docs/aidlc-state.md`
- Update the "Current Status" section
- Prepare for transition to CONSTRUCTION PHASE

---

## Critical Rules

- **NO HARDCODED LOGIC**: Adapt unit decomposition to the project's actual architecture and needs
- **VERIFY COMPLETION**: Ensure all unit artifacts are complete before presenting for approval
- **STORY COVERAGE**: Every story must be assigned to exactly one unit
- **EXPLICIT APPROVAL REQUIRED**: User must approve units before proceeding
- **USE APPLICATION DESIGN**: Unit boundaries must align with the component and service structure from Application Design
