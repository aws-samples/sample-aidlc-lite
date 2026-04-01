# Functional Design

## Purpose
**Detailed business logic design per unit**

Functional Design focuses on:
- Detailed business logic and algorithms for the unit
- Domain models with entities and relationships
- Detailed business rules, validation logic, and constraints
- Technology-agnostic design (no infrastructure concerns)

**Note**: This builds upon high-level component design from Application Design (INCEPTION phase)

## Prerequisites
- Units Generation must be complete
- Unit of work artifacts must be available
- Application Design recommended (provides high-level component structure)
- Execution plan must indicate Functional Design stage should execute

## Overview
Design detailed business logic for the unit, technology-agnostic and focused purely on business functions.

## Steps to Execute

### Step 1: Analyze Unit Context
- Read unit definition from `aidlc-docs/inception/application-design/unit-of-work.md`
- Read assigned stories from `aidlc-docs/inception/application-design/unit-of-work-story-map.md`
- Understand unit responsibilities and boundaries

### Step 2: Create Functional Design Plan
- Generate plan with checkboxes [] for functional design
- Focus on business logic, domain models, business rules
- Each step should have a checkbox []

### Step 3: Generate Context-Appropriate Questions
Ask 3-5 questions on the categories most relevant to this unit. Skip categories where the answer is evident from requirements, stories, or application design artifacts. Focus on areas where clarification would genuinely change the design.

- EMBED questions using [Answer]: tag format
- Only ask where user input would materially improve the functional design

**Suggested question categories** (pick the most relevant):
- **Business Logic Modeling** - Core entities, workflows, data transformations, and business processes
- **Domain Model** - Domain concepts, entity relationships, data structures, and business objects
- **Business Rules** - Decision rules, validation logic, constraints, and business policies
- **Data Flow** - Data inputs, outputs, transformations, and persistence requirements
- **Integration Points** - External system interactions, APIs, and data exchange
- **Error Handling** - Error scenarios, validation failures, and exception handling
- **Business Scenarios** - Edge cases, alternative flows, and complex business situations

### Step 4: Store Plan
- Save as `aidlc-docs/construction/plans/{unit-name}-functional-design-plan.md`
- Include all [Answer]: tags for user input

### Step 5: Collect and Analyze Answers
- Wait for user to complete all [Answer]: tags
- Review responses. If critical design points are ambiguous, ask up to 2 targeted clarifications in the same plan document. Then proceed.

### Step 6: Generate Functional Design Artifacts
- Create `aidlc-docs/construction/{unit-name}/functional-design/business-logic-model.md`
- Create `aidlc-docs/construction/{unit-name}/functional-design/business-rules.md`
- Create `aidlc-docs/construction/{unit-name}/functional-design/domain-entities.md`

### Step 7: Present Completion Message
- Present completion message in this structure:
     1. **Completion Announcement** (mandatory): Always start with this:

```markdown
# Functional Design Complete - [unit-name]
```

     2. **AI Summary** (optional): Provide structured bullet-point summary of functional design
        - Format: "Functional design has created [description]:"
        - List key business logic models and entities (bullet points)
        - List business rules and validation logic defined
        - Mention domain model structure and relationships
        - DO NOT include workflow instructions ("please review", "let me know", "proceed to next phase")
        - Keep factual and content-focused
     3. **Formatted Workflow Message** (mandatory): Always end with this exact format:

```markdown
> **REVIEW REQUIRED:**
> Please examine the functional design artifacts at: `aidlc-docs/construction/[unit-name]/functional-design/`

> **WHAT'S NEXT?**
>
> **You may:**
>
> **Request Changes** - Ask for modifications to the functional design based on your review
> **Continue to Next Stage** - Approve functional design and proceed to **[next-stage-name]**
```

### Step 8: Wait for Explicit Approval
- Do not proceed until the user explicitly approves the functional design
- Approval must be clear and unambiguous
- If user requests changes, update the design and repeat the approval process

### Step 9: Record Approval and Update Progress
- Log approval in audit.md with timestamp
- Record the user's approval response with timestamp
- Mark Functional Design stage complete in aidlc-state.md
