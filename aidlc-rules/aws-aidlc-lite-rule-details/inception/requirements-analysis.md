# Requirements Analysis (Adaptive)

**Assume the role** of a product owner

**Adaptive Phase**: Always executes. Detail level adapts to problem complexity.

**See [depth-levels.md](../common/depth-levels.md) for adaptive depth explanation**

## Prerequisites
- Workspace Detection must be complete
- Reverse Engineering must be complete (if brownfield)

## Execution Steps

### Step 1: Load Reverse Engineering Context (if available)

**IF brownfield project**:
- Load `aidlc-docs/inception/reverse-engineering/system-overview.md`
- Load `aidlc-docs/inception/reverse-engineering/api-and-dependencies.md`
- Use these to understand existing system when analyzing request

### Step 2: Analyze User Request (Intent Analysis)

#### 2.1 Request Clarity
- **Clear**: Specific, well-defined, actionable
- **Vague**: General, ambiguous, needs clarification
- **Incomplete**: Missing key information

#### 2.2 Request Type
- **New Feature**: Adding new functionality
- **Bug Fix**: Fixing existing issue
- **Refactoring**: Improving code structure
- **Upgrade**: Updating dependencies or frameworks
- **Migration**: Moving to different technology
- **Enhancement**: Improving existing feature
- **New Project**: Starting from scratch

#### 2.3 Initial Scope Estimate
- **Single File**: Changes to one file
- **Single Component**: Changes to one component/package
- **Multiple Components**: Changes across multiple components
- **System-wide**: Changes affecting entire system
- **Cross-system**: Changes affecting multiple systems

#### 2.4 Initial Complexity Estimate
- **Trivial**: Simple, straightforward change
- **Simple**: Clear implementation path
- **Moderate**: Some complexity, multiple considerations
- **Complex**: Significant complexity, many considerations

### Step 3: Determine Requirements Depth

**Based on request analysis, determine depth:**

**Minimal Depth** - Use when:
- Request is clear and simple
- No detailed requirements needed
- Just document the basic understanding

**Standard Depth** - Use when:
- Request needs clarification
- Functional and non-functional requirements needed
- Normal complexity

**Comprehensive Depth** - Use when:
- Complex project with multiple stakeholders
- High risk or critical system
- Detailed requirements with traceability needed

### Step 4: Assess Current Requirements

Analyze whatever the user has provided:
   - Intent statements or descriptions (already logged in audit.md)
   - Existing requirements documents (search workspace if mentioned)
   - Pasted content or file references
   - Convert any non-markdown documents to markdown format

### Step 5: Thorough Completeness Analysis

**CRITICAL**: Use comprehensive analysis to evaluate requirements completeness. Default to asking questions when there is ANY ambiguity or missing detail.

Evaluate these areas, focusing on those most relevant to the request. For clear requests, a brief analysis suffices:
- **Functional Requirements**: Core features, user interactions, system behaviors
- **Non-Functional Requirements**: Performance, security, scalability, usability
- **User Scenarios**: Use cases, user journeys, edge cases, error scenarios
- **Business Context**: Goals, constraints, success criteria, stakeholder needs
- **Technical Context**: Integration points, data requirements, system boundaries
- **Quality Attributes**: Reliability, maintainability, testability, accessibility

**When in doubt, ask questions** - incomplete requirements lead to poor implementations.

### Step 6: Generate Clarifying Questions (PROACTIVE APPROACH)
   - Create `aidlc-docs/inception/requirements/requirements-questions.md` only when the request has genuine ambiguity that would lead to wrong implementation direction. For clear, specific requests, proceed directly to generating the requirements document.
   - **MANDATORY — Archive before create**: ALWAYS follow this sequence before writing a new questions file:
     1. Read `aidlc-state.md` to get the prior project name (used to derive the archive slug: lowercase, spaces → hyphens, strip special characters).
     2. If `aidlc-docs/inception/requirements/requirements-questions.md` already exists:
        - If the prior task is **not marked complete** in `aidlc-state.md`: STOP. Warn the user that starting a new task will archive and close the prior one. Ask them to choose: **Resume** the prior task, or **Start New Task** (explicit confirmation required before archiving).
        - Read the existing file, then write its contents to `aidlc-docs/inception/requirements/requirements-questions.{prior-project-slug}.archived.md`.
        - Then create the new `requirements-questions.md` for the current task.
     3. If no prior file exists: create `requirements-questions.md` directly.
     Regardless, all question text MUST be captured verbatim in `audit.md` (see Step 9) — `audit.md` is append-only and is the single durable historical record.
   - Ask questions about ANY missing, unclear, or ambiguous areas
   - Focus on functional requirements, non-functional requirements, user scenarios, and business context
   - Request user to fill in all [Answer]: tags directly in the questions document
   - If presenting multiple-choice options for answers:
     - Label the options as A, B, C, D etc.
     - Ensure options are mutually exclusive and don't overlap
     - ALWAYS include option for custom response: "X) Other (please describe after [Answer]: tag below)"
   - Wait for user answers in the document
   - Analyze answers. If critical ambiguity remains that would affect architecture or core functionality, ask up to 3 targeted follow-up questions in the same file. Then proceed.

### Step 7: Generate Requirements Document

> **⚠️ CRITICAL — FILENAME RULE: The output MUST always be `requirements.md`. NEVER write a project-named variant such as `requirements.{project}.md` or `requirements.notes-something.md`. The archive step below is what captures history; a misnamed current file breaks session continuity.**

   - **MANDATORY — Archive before create**: ALWAYS follow this sequence before writing a new requirements document:
     1. If `aidlc-docs/inception/requirements/requirements.md` already exists:
        - Read the existing file, then write its contents to `aidlc-docs/inception/requirements/requirements.{prior-project-slug}.archived.md` (same slug derived in Step 6).
        - Then create the new `requirements.md` for the current task.
     2. If no prior file exists: create `requirements.md` directly.
   - Include intent analysis summary at the top:
     - User request
     - Request type
     - Scope estimate
     - Complexity estimate
   - Include both functional and non-functional requirements
   - Incorporate user's answers to clarifying questions
   - Provide brief summary of key requirements

### Step 8: Update State Tracking

Update `aidlc-docs/aidlc-state.md`:

```markdown
## Stage Progress
### INCEPTION PHASE
- [x] Workspace Detection
- [x] Reverse Engineering (if applicable)
- [x] Requirements Analysis
```

### Step 9: Log and Proceed
   - Log approval prompt with timestamp in `aidlc-docs/audit.md`
   - **MANDATORY — Self-contained Q&A logging**: When clarifying questions were used (Step 6), the audit entry for the answers MUST include the **full text of every question** alongside the user's answer (and any presented multiple-choice options). Do NOT log answers alone (e.g. "Q1: 4"). Reason: although `requirements-questions.md` is archived (not deleted) when a new task starts, the audit log is the canonical durable record — archive files may be cleaned up over time.
   - Suggested format:
```markdown
## Requirements Analysis — User Answers Received
**Timestamp**: [ISO timestamp]
**Questions & Answers** (full Q text retained; `requirements-questions.md` is archived on each new task):

- **Q1**: [Full question text]
  - 1) [Option 1 text]
  - 2) [Option 2 text]
  - ...
  - **Answer**: "[User's complete raw answer]"

- **Q2**: ...
```
   - Present completion message in this structure:
     1. **Completion Announcement** (mandatory): Always start with this:

```markdown
# Requirements Analysis Complete
```

     2. **AI Summary** (optional): Provide structured bullet-point summary of requirements
        - Format: "Requirements analysis has identified [project type/complexity]:"
        - List key functional requirements (bullet points)
        - List key non-functional requirements (bullet points)
        - Mention architectural considerations or technical decisions if relevant
        - DO NOT include workflow instructions ("please review", "let me know", "proceed to next phase", "before we proceed")
        - Keep factual and content-focused
     3. **Formatted Workflow Message** (mandatory): Always end with this exact format:

```markdown
> **REVIEW REQUIRED:**
> Please examine the requirements document at: `aidlc-docs/inception/requirements/requirements.md`

> **WHAT'S NEXT?**
>
> **You may:**
>
> **Request Changes** - Ask for modifications to the requirements if required based on your review
> [IF User Stories will be skipped, add this option:]
> **Add User Stories** - Choose to Include **User Stories** stage (currently skipped based on project simplicity)
> **Approve & Continue** - Approve requirements and proceed to **[User Stories/Workflow Planning]**
```

**Note**: Include the "Add User Stories" option only when User Stories stage will be skipped. Replace [User Stories/Workflow Planning] with the actual next stage name.

   - Wait for explicit user approval before proceeding
   - Record approval response with timestamp
   - Update Requirements Analysis stage complete in aidlc-state.md
