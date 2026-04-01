# AI-DLC Lite -- Core Rules

## 1. Process Overview

### The Three-Phase Lifecycle
- **INCEPTION PHASE**: Planning and architecture -- determines WHAT to build and WHY
- **CONSTRUCTION PHASE**: Design, implementation, build and test -- determines HOW to build it
- **OPERATIONS PHASE**: Placeholder for future deployment and monitoring workflows

### The Adaptive Workflow
AI-DLC analyzes your request, workspace, and complexity to determine which stages are needed.

- **Always-execute stages**: Workspace Detection, Requirements Analysis (adaptive depth), Workflow Planning, Code Generation (per-unit), Build and Test
- **Conditional stages**: Reverse Engineering, User Stories, Application Design, Units Generation, per-unit design stages (Functional Design, NFR Requirements, NFR Design, Infrastructure Design)
- **No fixed sequences**: Stages execute in the order that makes sense for the specific task

### Workflow Diagram

```
User Request
    |
    v
+--INCEPTION PHASE---------------------------+
| Workspace Detection      [ALWAYS]          |
| Reverse Engineering       [CONDITIONAL]    |
| Requirements Analysis    [ALWAYS]          |
| User Stories              [CONDITIONAL]    |
| Workflow Planning        [ALWAYS]          |
| Application Design        [CONDITIONAL]    |
| Units Generation          [CONDITIONAL]    |
+--------------------------------------------+
    |
    v
+--CONSTRUCTION PHASE------------------------+
| Per-Unit Loop:                             |
|   Functional Design       [CONDITIONAL]    |
|   NFR Requirements        [CONDITIONAL]    |
|   NFR Design              [CONDITIONAL]    |
|   Infrastructure Design   [CONDITIONAL]    |
| Code Generation          [ALWAYS]          |
| Build and Test           [ALWAYS]          |
+--------------------------------------------+
    |
    v
+--OPERATIONS PHASE--------------------------+
| Operations                [PLACEHOLDER]    |
+--------------------------------------------+
```

### Stage Details

| Stage | Phase | Execution | Description |
|---|---|---|---|
| Workspace Detection | INCEPTION | ALWAYS | Analyze workspace state and project type |
| Reverse Engineering | INCEPTION | CONDITIONAL | Analyze existing codebase (brownfield only) |
| Requirements Analysis | INCEPTION | ALWAYS | Gather and validate requirements (adaptive depth) |
| User Stories | INCEPTION | CONDITIONAL | Create user stories and personas |
| Workflow Planning | INCEPTION | ALWAYS | Create execution plan |
| Application Design | INCEPTION | CONDITIONAL | High-level component and service layer design |
| Units Generation | INCEPTION | CONDITIONAL | Decompose into units of work |
| Functional Design | CONSTRUCTION | CONDITIONAL | Detailed business logic design (per-unit) |
| NFR Requirements | CONSTRUCTION | CONDITIONAL | Determine NFRs and select tech stack (per-unit) |
| NFR Design | CONSTRUCTION | CONDITIONAL | Incorporate NFR patterns and logical components (per-unit) |
| Infrastructure Design | CONSTRUCTION | CONDITIONAL | Map to actual infrastructure services (per-unit) |
| Code Generation | CONSTRUCTION | ALWAYS | Generate code with planning then generation (per-unit) |
| Build and Test | CONSTRUCTION | ALWAYS | Build all units and execute comprehensive testing |
| Operations | OPERATIONS | PLACEHOLDER | Future deployment and monitoring workflows |

### Key Principles
- Each phase is independently evaluated; phases execute only when they add value
- INCEPTION focuses on "what" and "why"; CONSTRUCTION focuses on "how" plus "build and test"
- Simple changes may skip conditional stages; complex changes get full treatment

---

## 2. Terminology

### Phase vs Stage
**Phase**: One of the three high-level lifecycle phases (INCEPTION, CONSTRUCTION, OPERATIONS).
**Stage**: An individual workflow activity within a phase with specific prerequisites, steps, and outputs. Stages are ALWAYS-EXECUTE or CONDITIONAL. Do not confuse the terms: "Requirements Analysis" is a stage, not a phase; "CONSTRUCTION" is a phase, not a stage.

### Application Design Terms
- **Component**: A functional unit with specific responsibilities
- **Method**: A function or operation within a component with defined business rules
- **Business Rule**: Logic that governs method behavior and validation
- **Service**: Orchestration layer that coordinates business logic across components
- **Component Dependency**: Relationship and communication pattern between components

### Architecture Terms
- **Unit of Work**: A logical grouping of user stories for development purposes, used during planning and decomposition
- **Service**: An independently deployable component in a microservices architecture
- **Module**: A logical grouping of functionality within a single service or monolith (not independently deployable)
- **Component**: A reusable building block (class, function, or package) within a service or module

### Artifact Types
- **Plans**: Documents with checkboxes and questions that guide execution. Located in `aidlc-docs/plans/`
- **Artifacts**: Generated outputs from executing plans. Located in various `aidlc-docs/` subdirectories
- **State Files**: `aidlc-state.md` (overall workflow state) and `audit.md` (complete audit trail)

### Depth Levels
- **Minimal**: Quick, focused execution for simple changes
- **Standard**: Normal depth with standard artifacts for typical projects
- **Comprehensive**: Full depth with all artifacts for complex/high-risk projects

### Common Abbreviations
- **AI-DLC**: AI-Driven Development Life Cycle
- **NFR**: Non-Functional Requirements
- **UOW**: Unit of Work
- **CDK**: Cloud Development Kit (AWS)

---

## 3. Welcome & Orientation

### What is AI-DLC?
AI-DLC is a structured yet flexible software development process that adapts to your project's needs. It analyzes requirements, plans the optimal approach based on complexity and risk, skips unnecessary steps for simple changes, documents all decisions, and guides you through each phase with clear checkpoints.

### Key Principles
- **Fully Adaptive**: Each stage independently evaluated based on your needs
- **Efficient**: Simple changes execute only essential stages
- **Comprehensive**: Complex changes get full treatment with all safeguards
- **Transparent**: You see and approve the execution plan before work begins
- **Documented**: Complete audit trail of all decisions and changes
- **User Control**: You can request stages be included or excluded

### What Happens Next
1. Workspace analysis to understand if this is a new or existing project
2. Requirements gathering with clarifying questions if needed
3. Execution plan creation showing which stages to run and why
4. Review and approval of the plan (or request changes)
5. Plan execution with checkpoints at each major stage
6. Working code delivered with complete documentation and tests

---

## 4. Adaptive Depth

### Core Principle
**When a stage executes, ALL its defined artifacts are created. The "depth" refers to the level of detail and rigor within those artifacts, which adapts to the problem's complexity.**

### Stage Selection (Binary)
- Workflow Planning decides: EXECUTE or SKIP for each stage
- If EXECUTE: Stage runs and creates ALL its defined artifacts
- If SKIP: Stage does not run at all

### Detail Level (Adaptive)
- Simple problems get concise artifacts with essential detail
- Complex problems get comprehensive artifacts with extensive detail
- The model decides based on problem characteristics, not prescriptive rules

### Factors Influencing Detail Level
1. **Request Clarity**: How clear and complete is the user's request?
2. **Problem Complexity**: How intricate is the solution space?
3. **Scope**: Single file, component, multiple components, or system-wide?
4. **Risk Level**: What is the impact of errors or omissions?
5. **Available Context**: Greenfield vs brownfield, existing documentation
6. **User Preferences**: Has the user expressed preference for brevity or detail?

### Guiding Principle
**"Create exactly the detail needed for the problem at hand -- no more, no less."**
- Do not artificially inflate simple problems with unnecessary detail
- Do not shortchange complex problems by omitting critical detail
- Let problem characteristics drive detail level naturally

---

## 5. Questioning Philosophy

### Guiding Principles
1. **Default to Asking for High-Impact Decisions**: When ambiguity could lead to wrong implementation direction, ask. For low-impact decisions, note your assumption and proceed.
2. **Comprehensive Coverage**: Evaluate ALL relevant categories; do not skip areas
3. **Thorough Analysis**: Carefully analyze ALL user responses for ambiguities
4. **Mandatory Follow-up**: Create follow-up questions for ANY unclear responses
5. **Resolve Critical Ambiguity**: Do not proceed when unclear on architecture, scope, or core requirements. For lower-impact details, state assumption and move forward.

### Implementation Guidelines

**For Question Generation**:
- Evaluate ALL question categories; do not skip any
- Ask questions wherever clarification would improve quality
- Include comprehensive question categories in each stage
- Ask when ambiguity has high impact; prefer reasonable defaults for low-impact decisions

**For Answer Analysis**:
- Look for vague responses: "depends", "maybe", "not sure", "mix of", "somewhere between"
- Detect undefined terms and references to external concepts
- Identify contradictory or incomplete answers
- Create follow-up questions for ANY ambiguities

**For Follow-up Questions**:
- Create separate clarification files when ambiguities are detected
- Ask specific questions to resolve each ambiguity
- Do not proceed on high-impact items until unclear responses are clarified

### Quality Assurance

**Red Flags**:
- Stages completing without asking any questions on complex projects
- Proceeding with vague or ambiguous user responses
- Skipping entire question categories without justification
- Making assumptions on high-impact decisions instead of asking for clarification

**Success Indicators**:
- Appropriate number of clarifying questions for project complexity
- Thorough analysis of user responses with follow-up when needed
- Clear, unambiguous requirements before proceeding to implementation
- Reduced need for changes during later stages due to better upfront clarification

### Key Takeaway
**It is better to ask too many questions than to make incorrect assumptions.** The cost of asking clarifying questions upfront is far less than the cost of implementing the wrong solution. For low-impact decisions, state your assumption explicitly and proceed.

---

## 6. Session Continuity

### Welcome Back Prompt Template
When a user returns to continue work on an existing AI-DLC project, present:

```markdown
**Welcome back! I can see you have an existing AI-DLC project in progress.**

Based on your aidlc-state.md, here's your current status:
- **Project**: [project-name]
- **Current Phase**: [INCEPTION/CONSTRUCTION/OPERATIONS]
- **Current Stage**: [Stage Name]
- **Last Completed**: [Last completed step]
- **Next Step**: [Next step to work on]

**What would you like to work on today?**

A) Continue where you left off ([Next step description])
B) Review a previous stage ([Show available stages])

[Answer]:
```

### MANDATORY: Session Continuity Instructions
1. **Always read aidlc-state.md first** when detecting an existing project
2. **Parse current status** from the workflow file to populate the prompt
3. **MANDATORY: Load Previous Stage Artifacts** -- Before resuming any stage, automatically read all relevant artifacts from previous stages:
   - **Reverse Engineering**: Read architecture.md, code-structure.md, api-documentation.md
   - **Requirements Analysis**: Read requirements.md, requirement-verification-questions.md
   - **User Stories**: Read stories.md, personas.md, story-generation-plan.md
   - **Application Design**: Read application-design artifacts (components.md, component-methods.md, services.md)
   - **Design (Units)**: Read unit-of-work.md, unit-of-work-dependency.md, unit-of-work-story-map.md
   - **Per-Unit Design**: Read functional-design.md, nfr-requirements.md, nfr-design.md, infrastructure-design.md
   - **Code Stages**: Read all code files, plans, AND all previous artifacts
4. **Smart Context Loading by Stage**:
   - **Early Stages** (Workspace Detection, Reverse Engineering): Load workspace analysis
   - **Requirements/Stories**: Load reverse engineering + requirements artifacts
   - **Design Stages**: Load requirements + stories + architecture + design artifacts
   - **Code Stages**: Load ALL artifacts + existing code files
5. **Adapt options** based on architectural choice and current phase
6. **Show specific next steps** rather than generic descriptions
7. **Log the continuity prompt** in audit.md with timestamp
8. **Context Summary**: After loading artifacts, provide brief summary of what was loaded
9. **Asking questions**: ALWAYS ask clarification or user feedback questions by placing them in .md files. DO NOT place multiple-choice questions inline in the chat session.

### Error Handling
If artifacts are missing or corrupted during session resumption, see the Error Handling & Recovery section below.

---

## 7. Mid-Workflow Changes

### 1. Adding a Skipped Stage
**Trigger**: User wants to add a stage that was originally skipped.
**Steps**:
1. Confirm request and explain what the stage will produce
2. Check that all prerequisite stages are complete
3. Add stage to execution plan with rationale
4. Mark as PENDING in aidlc-state.md, execute, and log in audit.md
**Key risk**: Later stages may need updating to incorporate new artifacts.

### 2. Skipping a Planned Stage
**Trigger**: User wants to skip a stage that was planned to execute.
**Steps**:
1. Confirm request and warn about what will be missing
2. Get explicit confirmation that user understands the impact
3. Mark as SKIPPED in aidlc-state.md and execution plan
4. Adjust later stages that depended on skipped artifacts; log in audit.md
**Key risk**: Later stages may fail or require manual intervention due to missing artifacts.

### 3. Restarting Current Stage
**Trigger**: User is unhappy with current stage results.
**Steps**:
1. Understand the specific concern
2. Offer modification of existing artifacts (faster) or complete restart (clean slate)
3. If restart: archive existing artifacts, reset checkboxes, re-execute from beginning
4. Log reason and impact in audit.md
**Key risk**: Existing work is lost (though backed up); dependent stages may need redo.

### 4. Restarting a Previous Stage
**Trigger**: User wants to go back and redo a completed stage.
**Steps**:
1. Identify all stages that depend on the target stage
2. Warn user about full cascade of rework required
3. Get explicit confirmation
4. Archive all affected artifacts, reset all affected stages, re-execute from target stage
**Key risk**: Significant rework; all dependent stages must be redone.

### 5. Changing Stage Depth
**Trigger**: User wants to change the depth level (minimal/standard/comprehensive).
**Steps**:
1. Confirm the change and explain time/quality tradeoff
2. Update depth in workflow-planning.md
3. Adjust approach and inform user of new timeline
4. Log the change in audit.md
**Key risk**: Can only change before or during a stage, not after completion.

### 6. Pausing Workflow
**Trigger**: User needs to stop and resume later.
**Steps**:
1. Complete current step if possible
2. Update all checkboxes and ensure aidlc-state.md reflects current status
3. Log pause point in audit.md
4. On resume: detect project, load context, show status, offer continue or review options
**Key risk**: Context loss between sessions; mitigated by state files and artifacts.

### 7. Changing Architectural Decision
**Trigger**: User wants to change architecture (e.g., monolith to microservices).
**Steps**:
1. Assess current progress to determine impact scope
2. Explain impact: before Units Planning = minimal; after Code Generation = significant rework
3. Recommend restart from Application Design or evaluate if modification is feasible
4. Get confirmation, execute change following restart procedures
**Key risk**: Cascading effects on all downstream stages; earlier change = easier.

### 8. Adding/Removing Units
**Trigger**: User wants to add, remove, or split units after Units Generation.
**Steps**:
1. Assess which units have completed design/code
2. Explain consequences: new units need full design; removed units need functionality redistributed
3. Update unit-of-work.md, dependency, and story-map artifacts
4. Mark affected units for redesign; execute normal design and code process
**Key risk**: Affects all downstream stages for those units and potentially their dependencies.

### Change Request Decision Tree

```
User requests change
    |
    +-- Current stage? --> Modify or restart current stage
    +-- Completed stage? --> Assess dependent stages
    |       +-- Low impact --> Modify and update dependents
    |       +-- High impact --> Restart from that stage
    +-- Adding skipped stage? --> Check prerequisites, add, execute
    +-- Skipping planned stage? --> Warn impact, confirm, skip
    +-- Changing depth? --> Update plan, adjust approach
    +-- None of the above --> Clarify request with user
```

### General Guidelines
**Before**: Understand request, assess impact, explain consequences, offer alternatives, get explicit confirmation.
**During**: Archive before destructive changes, keep all tracking files in sync, validate consistency.
**After**: Verify artifact alignment, update documentation, log in audit.md, confirm with user.

---

## 8. Error Handling & Recovery

### General Error Handling Principles
1. **Identify** the error: clearly state what went wrong
2. **Assess** impact: determine if blocking or can be worked around
3. **Communicate**: inform the user about the error and options
4. **Offer solutions**: provide clear steps to resolve or work around
5. **Document**: log the error and resolution in audit.md

### Error Severity Levels
- **Critical** (workflow blocked): Missing required files, invalid input, system errors
- **High** (stage blocked): Incomplete answers, contradictory responses, missing dependencies
- **Medium** (workaround available): Optional artifacts missing, non-critical validation failures
- **Low** (non-blocking): Formatting inconsistencies, optional information missing

### General Phase Error Pattern
1. Identify the error and severity
2. If Critical: Stop, inform user, offer recovery options
3. If High: Create follow-up questions or request missing input
4. If Medium: Apply workaround, document, continue
5. If Low: Log, continue

### Phase-Specific Exceptions

| Phase | Common Error | Resolution |
|---|---|---|
| Workspace Detection | Cannot read workspace files | Ask user to verify path and permissions |
| Workspace Detection | Corrupted aidlc-state.md | Backup + rebuild from artifacts |
| Requirements Analysis | Contradictory requirements | Follow-up questions to resolve; do not proceed |
| Requirements Analysis | Incomplete answers | Highlight unanswered questions with examples |
| Application Design | Unclear architectural decision | Follow-up questions; do not proceed until clear |
| Units/Design | Circular unit dependencies | Identify cycles, suggest refactoring boundaries |
| NFR Implementation | Incompatible tech stack choices | Highlight incompatibilities, ask user to choose |
| Code Generation | Syntax errors in output | Fix and revalidate before proceeding |
| Code Generation | Missing design artifacts | Return to design stage to complete |
| Operations | Unclear build tool or deploy target | Ask user to specify; provide generic fallback |

### Recovery Procedures
- **Partial Completion**: Load plan file, find last checked step, verify prior steps, resume from next uncompleted step
- **Corrupted State File**: Backup, ask user which phase they are on, regenerate from artifacts, resume
- **Missing Artifacts**: Identify gap, return to originating stage or ask user for manual input, document in audit.md
- **Restart Request**: Confirm with user, archive artifacts, reset aidlc-state.md, re-execute
- **Skip Request**: Confirm user understands implications, mark SKIPPED in audit.md and state, proceed

### Escalation Guidelines
**Ask user for help immediately** when: contradictory input, missing required information, technical constraints AI cannot resolve, business judgment needed. **Ask after attempting resolution** when: repeated errors, complex technical issues, unusual project structures. **Suggest starting over** when: multiple stages have errors, state file is severely corrupted, artifacts are inconsistent across stages.

### Session Resumption Errors
- **Missing artifacts**: Identify originating stage; if marked complete regenerate, otherwise resume from that stage
- **Empty/corrupted artifact**: Backup corrupted file, re-execute originating stage
- **State vs artifacts mismatch**: Reconcile by verifying actual artifacts, update state to match reality
- **Multiple stages marked current**: Review artifacts, ask user, correct state file

---

## 9. Content & Diagram Standards

### ASCII Diagram Rules
**Allowed characters**: `+` `-` `|` `^` `v` `<` `>` and alphanumeric text with spaces only. **Forbidden**: Unicode box-drawing characters -- they render inconsistently across platforms. **Character Width Rule**: Every line in a box MUST have EXACTLY the same character count (including spaces).

**Box Pattern Example**:
```
+-----------------------------------------------------+
|                                                     |
|              Calculator Application                 |
|                                                     |
|  Provides basic arithmetic operations for users     |
|  through a web-based interface                      |
|                                                     |
+-----------------------------------------------------+
```

### Mermaid Diagram Validation

**Required steps before creating any Mermaid diagram**:
1. Check for invalid characters in node IDs (use alphanumeric + underscore only)
2. Escape special characters in labels: `"` and `'`
3. Validate flowchart syntax: node connections must be valid
4. Test diagram parsing with simple validation

**Fallback**: If Mermaid validation fails, use a text-based workflow representation:
```
Phase 1: INCEPTION
- Stage 1: Workspace Detection (COMPLETED)
- Stage 2: Requirements Analysis (IN PROGRESS)
```

### Validation Failure Handling
1. Log what failed validation
2. Switch to text-based alternative
3. Continue workflow; do not block on content validation failures
4. Inform user that simplified content was used due to parsing constraints
