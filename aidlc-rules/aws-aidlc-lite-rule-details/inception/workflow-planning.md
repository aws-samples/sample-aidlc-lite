# Workflow Planning

**Purpose**: Determine which phases to execute and create comprehensive execution plan

**Always Execute**: This phase always runs after understanding requirements and scope

## Step 1: Load All Prior Context

### 1.1 Load Reverse Engineering Artifacts (if brownfield)
- system-overview.md
- api-and-dependencies.md

### 1.2 Load Requirements Analysis
- requirements.md (includes intent analysis)
- requirement-verification-questions.md (with answers)

### 1.3 Load User Stories (if executed)
- stories.md
- personas.md

## Step 2: Detailed Scope and Impact Analysis

**Now that we have complete context (requirements + stories), perform detailed analysis:**

### 2.1 Transformation Scope Detection (Brownfield Only)

**IF brownfield project**, analyze transformation scope:
- **Single component change** vs **architectural transformation**
- **Infrastructure changes** vs **application changes**
- **Deployment model changes** (Lambda to Container, EC2 to Serverless, etc.)
- Check for impacts on infrastructure code, CDK stacks, and dependent packages

### 2.2 Change Impact Assessment

Evaluate impact across these areas:
- **User-facing changes**: Does this affect user experience?
- **Structural changes**: Does this change system architecture?
- **Data model changes**: Does this affect database schemas or data structures?
- **API changes**: Does this affect interfaces or contracts?
- **NFR impact**: Does this affect performance, security, or scalability?
- **Application layer**: Code changes, dependencies, configuration, testing
- **Infrastructure layer**: Deployment model, networking, storage, scaling
- **Operations layer**: Monitoring, logging, alerting, deployment pipelines

### 2.3 Component Relationships (Brownfield Only)

For brownfield: map component dependencies including infrastructure, shared, and dependent packages. For each related component identify change type (Major/Minor/Configuration-only), change reason, and change priority.

### 2.4 Risk Assessment

Evaluate risk level:
1. **Low**: Isolated change, easy rollback, well-understood
2. **Medium**: Multiple components, moderate rollback, some unknowns
3. **High**: System-wide impact, complex rollback, significant unknowns
4. **Critical**: Production-critical, difficult rollback, high uncertainty

## Step 3: Phase Determination

### 3.1 User Stories - Already Executed or Skip?
**Already executed**: Move to next determination
**Not executed - Execute IF**: Multiple user personas, user experience impact, acceptance criteria needed, team collaboration required
**Skip IF**: Internal refactoring, bug fix with clear reproduction, technical debt reduction, infrastructure changes

### 3.2 Application Design - Execute IF:
- New components or services needed
- Component methods and business rules need definition
- Service layer design required
- Component dependencies need clarification

**Skip IF**: Changes within existing component boundaries, no new components or methods, pure implementation changes

### 3.3 Design (Units Planning/Generation) - Execute IF:
- New data models or schemas
- API changes or new endpoints
- Complex algorithms or business logic
- Multiple packages require changes
- Infrastructure-as-code updates needed

**Skip IF**: Simple logic changes, UI-only changes, configuration updates, straightforward implementations

### 3.4 NFR Implementation - Execute IF:
- Performance requirements
- Security considerations
- Scalability concerns
- Monitoring/observability needed

**Skip IF**: Existing NFR setup sufficient, no new NFR requirements, simple changes with no NFR impact

## Step 4: Note Adaptive Detail

**See [depth-levels.md](../common/depth-levels.md) for adaptive depth explanation**

For each stage that will execute:
- All defined artifacts will be created
- Detail level within artifacts adapts to problem complexity
- Model determines appropriate detail based on problem characteristics

## Step 5: Multi-Module Coordination Analysis (Brownfield Only)

**IF brownfield with multiple modules/packages**, analyze dependencies and determine optimal update strategy:

- Examine build system dependencies and dependency manifests
- Identify build-time vs runtime dependencies
- Map API contracts and shared interfaces between modules
- Determine update sequence, parallelization opportunities, and coordination requirements
- Document testing strategy and rollback strategy

## Step 6: Generate Workflow Visualization

Create Mermaid flowchart showing:
- All phases in sequence
- EXECUTE or SKIP decision for each conditional phase
- Proper styling for each phase state

**Style Guidelines**: Use Material Design colors - Green for completed/always-execute phases, Orange (dashed) for conditional execute, Gray (dashed) for conditional skip, Purple for start/end nodes. Use lighter colors for phase containers (INCEPTION: blue, CONSTRUCTION: green, OPERATIONS: yellow).

## Step 7: Create Execution Plan Document

Create `aidlc-docs/inception/plans/execution-plan.md` containing:

- **Detailed Analysis Summary**: Transformation scope (brownfield), change impact assessment, component relationships (brownfield), risk assessment
- **Workflow Visualization**: Mermaid flowchart with all phases and status indicators
- **Phases to Execute**: Checklist of all phases across INCEPTION, CONSTRUCTION, and OPERATIONS with status (COMPLETED/EXECUTE/SKIP) and rationale for each
- **Package Change Sequence** (brownfield only): Module update order with dependencies
- **Estimated Timeline**: Total phases, estimated duration
- **Success Criteria**: Primary goal, key deliverables, quality gates

## Step 8: Initialize State Tracking

Update `aidlc-docs/aidlc-state.md` with:
- Project information (type, start date, current stage)
- Execution plan summary (total stages, stages to execute, stages to skip with reasons)
- Stage progress checklist across all phases (INCEPTION, CONSTRUCTION, OPERATIONS)
- Current status (lifecycle phase, current stage, next stage, status)

## Step 9: Present Plan to User

```markdown
# Workflow Planning Complete

I've created a comprehensive execution plan based on:
- Your request: [Summary]
- Existing system: [Summary if brownfield]
- Requirements: [Summary if executed]
- User stories: [Summary if executed]

**Detailed Analysis**:
- Risk level: [Level]
- Impact: [Summary of key impacts]
- Components affected: [List]

**Recommended Execution Plan**:

I recommend executing [X] stages:
[List stages with rationale per phase]

I recommend skipping [Y] stages:
[List stages with rationale per phase]

[IF brownfield with multiple packages]
**Recommended Package Update Sequence**:
[Numbered list with reasons]

**Estimated Timeline**: [Duration]

> **REVIEW REQUIRED:**
> Please examine the execution plan at: `aidlc-docs/inception/plans/execution-plan.md`

> **WHAT'S NEXT?**
>
> **You may:**
>
> **Request Changes** - Ask for modifications to the execution plan if required
> [IF any stages are skipped:]
> **Add Skipped Stages** - Choose to include stages currently marked as SKIP
> **Approve & Continue** - Approve plan and proceed to **[Next Stage Name]**
```

## Step 10: Handle User Response

- **If approved**: Proceed to next stage in execution plan
- **If changes requested**: Update execution plan and re-confirm
- **If user wants to force include/exclude stages**: Update plan accordingly

## Step 11: Log Interaction

Log in `aidlc-docs/audit.md`:

```markdown
## Workflow Planning - Approval
**Timestamp**: [ISO timestamp]
**AI Prompt**: "Ready to proceed with this plan?"
**User Response**: "[User's COMPLETE RAW response]"
**Status**: [Approved/Changes Requested]
**Context**: Workflow plan created with [X] stages to execute

---
```
