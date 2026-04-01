# User Stories

## Purpose
**Convert requirements into user-centered stories with acceptance criteria**

User Stories focus on:
- Translating business requirements into user-centered narratives
- Defining clear acceptance criteria for each story
- Creating user personas that represent different stakeholder types
- Establishing shared understanding across teams
- Providing testable specifications for implementation

## Prerequisites
- Workspace Detection must be complete
- Requirements Analysis recommended (can reference requirements if available)
- Workflow Planning must indicate User Stories stage should execute

## Intelligent Assessment Guidelines

**WHEN TO EXECUTE USER STORIES**: Use this enhanced assessment before proceeding:

### High Priority Execution (ALWAYS Execute)
- **New User Features**: Any new functionality users will directly interact with
- **User Experience Changes**: Modifications to existing user workflows or interfaces
- **Multi-Persona Systems**: Applications serving different types of users
- **Customer-Facing APIs**: Services that external users or systems will consume
- **Complex Business Logic**: Requirements with multiple scenarios or business rules
- **Cross-Team Projects**: Work requiring shared understanding across multiple teams

### Medium Priority Execution (Assess Complexity)
- **Backend User Impact**: Internal changes that indirectly affect user experience
- **Performance Improvements**: Enhancements with user-visible benefits
- **Integration Work**: Connecting systems that affect user workflows
- **Data Changes**: Modifications affecting user data, reports, or analytics
- **Security Enhancements**: Changes affecting user authentication or permissions

### Skip Only For Simple Cases
- **Pure Refactoring**: Internal code improvements with zero user impact
- **Isolated Bug Fixes**: Simple, well-defined fixes with clear scope
- **Infrastructure Only**: Changes with no user-facing effects
- **Developer Tooling**: Build processes, CI/CD, or development environment changes
- **Documentation**: Updates that don't affect functionality

### Default Decision Rule
**When in doubt, include user stories.** The overhead of creating stories is typically outweighed by clearer requirements understanding, better testing criteria, and reduced implementation risks.

---

## Step 1: Validate User Stories Need

Before proceeding with user stories, perform this assessment:

1. **Analyze Request Context**: Review the original user request and requirements. Identify user-facing vs internal-only changes. Assess complexity, scope, and stakeholder involvement.
2. **Apply Assessment Criteria**: Check against High Priority indicators. Evaluate Medium Priority factors. Confirm this is not a simple case that should be skipped.
3. **Decide**: User stories must add clear value. If justified, proceed. If this is a simple skip case, document the reasoning briefly and move to the next stage.

## Step 2: Load Context

- Read `aidlc-docs/inception/requirements/requirements.md`
- Load any available reverse engineering artifacts (if brownfield)
- Load any prior inception artifacts that provide useful context

## Step 3: Generate Questions (If Needed)

Ask 3-5 high-impact questions covering the most relevant categories for this project. Categories to consider: User Personas, Story Granularity, Acceptance Criteria, User Journeys, Business Context.

- Create `aidlc-docs/inception/user-stories/story-questions.md` with questions using [Answer]: tag format
- Wait for user to provide answers
- If critical ambiguity remains, ask up to 2 targeted follow-ups in the same file. Then proceed.

For clear projects where the requirements already cover these areas well, this step may be skipped entirely.

## Step 4: Generate Stories and Personas

- Create `aidlc-docs/inception/user-stories/stories.md` following INVEST criteria:
  - Stories must be Independent, Negotiable, Valuable, Estimable, Small, Testable
  - Include acceptance criteria for each story
  - Organize stories logically (by feature, persona, or domain as appropriate)
- Create `aidlc-docs/inception/user-stories/personas.md`:
  - Define user archetypes with characteristics, goals, and pain points
  - Map personas to relevant user stories

## Step 5: Update State Tracking

Update `aidlc-docs/aidlc-state.md`:

```markdown
## Stage Progress
### INCEPTION PHASE
- [x] Workspace Detection
- [x] Reverse Engineering (if applicable)
- [x] Requirements Analysis
- [x] User Stories
```

## Step 6: Present Completion Message

Present completion message in this structure:
1. **Completion Announcement** (mandatory):

```markdown
# User Stories Complete
```

2. **AI Summary** (optional): Provide structured bullet-point summary of generated stories
   - Format: "User stories generation has created [description]:"
   - List key personas generated (bullet points)
   - List user stories created with counts and organization
   - Mention story structure and compliance (INVEST criteria, acceptance criteria)
   - DO NOT include workflow instructions
   - Keep factual and content-focused

3. **Formatted Workflow Message** (mandatory):

```markdown
> **REVIEW REQUIRED:**
> Please examine the user stories and personas at: `aidlc-docs/inception/user-stories/stories.md` and `aidlc-docs/inception/user-stories/personas.md`

> **WHAT'S NEXT?**
>
> **You may:**
>
> **Request Changes** - Ask for modifications to the stories or personas based on your review
> **Approve & Continue** - Approve user stories and proceed to **Workflow Planning**
```

## Step 7: Wait for Explicit Approval

- Do not proceed until the user explicitly approves the generated stories
- Approval must be clear and unambiguous
- If user requests changes, update stories and repeat the approval process

## Step 8: Record Approval and Update Progress

- Log the user's approval response with timestamp in `aidlc-docs/audit.md`
- Include the exact user response text
- Mark the approval status clearly
- Mark User Stories stage complete in `aidlc-state.md`
- Update the "Current Status" section
- Prepare for transition to next stage

---

# CRITICAL RULES

- **NO HARDCODED LOGIC**: Adapt story structure to the project's actual needs
- **FOLLOW INVEST CRITERIA**: Every story must be Independent, Negotiable, Valuable, Estimable, Small, Testable
- **VERIFY COMPLETION**: Ensure all story artifacts are complete before presenting for approval
- **EXPLICIT APPROVAL REQUIRED**: User must approve stories before proceeding
- **ACCEPTANCE CRITERIA**: Every story must have testable acceptance criteria
- **PERSONA MAPPING**: Every story must be associated with at least one persona
