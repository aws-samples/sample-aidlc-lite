# Code Generation

## Overview
Generate code for each unit of work in a single flow: analyze context, plan internally, generate code, and present for approval.

**Note**: For brownfield projects, "generate" means modify existing files when appropriate, not create duplicates.

## Prerequisites
- Unit Design Generation must be complete for the unit
- NFR Implementation (if executed) must be complete for the unit
- All unit design artifacts must be available
- Unit is ready for code generation

---

## Step 1: Analyze Unit Context
- Read unit design artifacts from Unit Design Generation
- Read unit story map to understand assigned stories
- Identify unit dependencies and interfaces
- Validate unit is ready for code generation
- Read workspace root and project type from `aidlc-docs/aidlc-state.md`

## Step 2: Create Internal Code Plan
Plan the code generation internally. Do not write a separate plan document for user approval.

- Determine code location (see Code Location Rules below)
- **Brownfield only**: Review reverse engineering code-structure.md for existing files to modify
- Plan generation steps internally:
  - Project Structure Setup (greenfield only)
  - Business Logic Generation
  - Business Logic Unit Testing
  - API Layer Generation
  - API Layer Unit Testing
  - Repository Layer Generation
  - Repository Layer Unit Testing
  - Database Migration Scripts (if data models exist)
  - Documentation Generation (API docs, README updates)
  - Deployment Artifacts Generation
- Document exact paths internally (never aidlc-docs/ for application code)
- Include story mapping references and dependency tracking

## Step 3: Execute Code Generation
Generate code step by step following the internal plan:

- **Brownfield**: Check if target file exists before generating
  - If exists: Modify in-place (never create copies like `ClassName_modified.java`)
  - If doesn't exist: Create new file
- **Greenfield**: Create new files per the planned structure
- Write application code to workspace root per project structure
- Write documentation to `aidlc-docs/construction/{unit-name}/code/` (markdown only)
- Write build/config files to workspace root
- Follow unit story requirements
- Respect dependencies and interfaces
- Verify no duplicate files created after generation

## Step 4: Update Progress
- Update `aidlc-docs/aidlc-state.md` current status
- Mark associated unit stories as complete when their generation is finished

## Step 5: Present Completion Message
- Present completion message in this structure:
     1. **Completion Announcement** (mandatory): Always start with this:

```markdown
# Code Generation Complete - [unit-name]
```

     2. **AI Summary** (optional): Provide structured bullet-point summary
        - **Brownfield**: Distinguish modified vs created files (e.g., "Modified: `src/services/user-service.ts`", "Created: `src/services/auth-service.ts`")
        - **Greenfield**: List created files with paths (e.g., "Created: `src/services/user-service.ts`")
        - List tests, documentation, deployment artifacts with paths
        - Keep factual, no workflow instructions
     3. **Formatted Workflow Message** (mandatory): Always end with this exact format:

```markdown
> **REVIEW REQUIRED:**
> Please examine the generated code at:
> - **Application Code**: `[actual-workspace-path]`
> - **Documentation**: `aidlc-docs/construction/[unit-name]/code/`

> **WHAT'S NEXT?**
>
> **You may:**
>
> **Request Changes** - Ask for modifications to the generated code based on your review
> **Continue to Next Stage** - Approve code generation and proceed to **[next-unit/Build & Test]**
```

## Step 6: Wait for Explicit Approval
- Do not proceed until the user explicitly approves the generated code
- Approval must be clear and unambiguous
- If user requests changes, update the code and repeat the approval process

## Step 7: Record Approval and Update Progress
- Log approval in audit.md with timestamp
- Record the user's approval response with timestamp
- Mark Code Generation stage as complete for this unit in aidlc-state.md

---

## Code Location Rules

- **Application code**: Workspace root only (NEVER aidlc-docs/)
- **Documentation**: aidlc-docs/ only (markdown summaries)
- **Read workspace root** from aidlc-state.md before generating code

**Structure patterns by project type**:
- **Brownfield**: Use existing structure (e.g., `src/main/java/`, `lib/`, `pkg/`)
- **Greenfield single unit**: `src/`, `tests/`, `config/` in workspace root
- **Greenfield multi-unit (microservices)**: `{unit-name}/src/`, `{unit-name}/tests/`
- **Greenfield multi-unit (monolith)**: `src/{unit-name}/`, `tests/{unit-name}/`

## Brownfield File Modification Rules

- Check if file exists before generating
- If exists: Modify in-place (never create copies like `ClassName_modified.java`)
- If doesn't exist: Create new file
- Verify no duplicate files after generation

## Critical Rules

- **NO HARDCODED LOGIC**: Only execute what was planned in the internal code plan
- **FOLLOW PLAN EXACTLY**: Do not deviate from the planned step sequence
- **STORY TRACEABILITY**: Mark unit stories as complete when functionality is implemented
- **RESPECT DEPENDENCIES**: Only implement when unit dependencies are satisfied

## Completion Criteria
- All planned generation steps executed
- All unit stories implemented according to plan
- All code and tests generated (tests will be executed in Build & Test phase)
- Deployment artifacts generated
- Complete unit ready for build and verification
