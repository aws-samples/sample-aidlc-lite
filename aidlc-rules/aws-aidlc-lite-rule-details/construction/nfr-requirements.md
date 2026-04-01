# NFR Requirements

## Prerequisites
- Functional Design must be complete for the unit
- Unit functional design artifacts must be available
- Execution plan must indicate NFR Requirements stage should execute

## Overview
Determine non-functional requirements for the unit and make tech stack choices.

## Steps to Execute

### Step 1: Analyze Functional Design
- Read functional design artifacts from `aidlc-docs/construction/{unit-name}/functional-design/`
- Understand business logic complexity and requirements

### Step 2: Create NFR Requirements Plan
- Generate plan with checkboxes [] for NFR assessment
- Focus on scalability, performance, availability, security
- Each step should have a checkbox []

### Step 3: Generate Context-Appropriate Questions
Ask 3-5 questions on the NFR categories most relevant to this project type. For prototypes and demos, focus on tech stack selection and basic performance. Skip detailed scalability/availability analysis unless the project specifically requires it.

- EMBED questions using [Answer]: tag format
- Only ask where user input would materially improve NFR and tech stack decisions

**Suggested question categories** (pick the most relevant):
- **Scalability Requirements** - Expected load, growth patterns, scaling triggers, and capacity planning
- **Performance Requirements** - Response times, throughput, latency, and performance benchmarks
- **Availability Requirements** - Uptime expectations, disaster recovery, failover, and business continuity
- **Security Requirements** - Data protection, compliance, authentication, authorization, and threat models
- **Tech Stack Selection** - Technology preferences, constraints, existing systems, and integration requirements
- **Reliability Requirements** - Error handling, fault tolerance, monitoring, and alerting needs
- **Maintainability Requirements** - Code quality, documentation, testing, and operational requirements
- **Usability Requirements** - User experience, accessibility, and interface requirements

### Step 4: Store Plan
- Save as `aidlc-docs/construction/plans/{unit-name}-nfr-requirements-plan.md`
- Include all [Answer]: tags for user input

### Step 5: Collect and Analyze Answers
- Wait for user to complete all [Answer]: tags
- Review responses. If tech stack decisions are ambiguous, ask up to 2 targeted clarifications. Then proceed.

### Step 6: Generate NFR Requirements Artifacts
- Create `aidlc-docs/construction/{unit-name}/nfr-requirements/nfr-requirements.md`
- Create `aidlc-docs/construction/{unit-name}/nfr-requirements/tech-stack-decisions.md`

### Step 7: Present Completion Message
- Present completion message in this structure:
     1. **Completion Announcement** (mandatory): Always start with this:

```markdown
# NFR Requirements Complete - [unit-name]
```

     2. **AI Summary** (optional): Provide structured bullet-point summary of NFR requirements
        - Format: "NFR requirements assessment has identified [description]:"
        - List key scalability, performance, availability requirements (bullet points)
        - List security and compliance requirements identified
        - Mention tech stack decisions and rationale
        - DO NOT include workflow instructions ("please review", "let me know", "proceed to next phase")
        - Keep factual and content-focused
     3. **Formatted Workflow Message** (mandatory): Always end with this exact format:

```markdown
> **REVIEW REQUIRED:**
> Please examine the NFR requirements at: `aidlc-docs/construction/[unit-name]/nfr-requirements/`

> **WHAT'S NEXT?**
>
> **You may:**
>
> **Request Changes** - Ask for modifications to the NFR requirements based on your review
> **Continue to Next Stage** - Approve NFR requirements and proceed to **[next-stage-name]**
```

### Step 8: Wait for Explicit Approval
- Do not proceed until the user explicitly approves the NFR requirements
- Approval must be clear and unambiguous
- If user requests changes, update the requirements and repeat the approval process

### Step 9: Record Approval and Update Progress
- Log approval in audit.md with timestamp
- Record the user's approval response with timestamp
- Mark NFR Requirements stage complete in aidlc-state.md
