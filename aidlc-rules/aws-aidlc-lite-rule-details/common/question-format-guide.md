# Question Format Guide (Lite)

## Rule: Never Ask Questions in Chat

ALL questions to the user MUST be placed in dedicated question files. Never ask questions directly in the chat interface. This ensures:
- Questions are tracked and documented
- Users can answer at their own pace
- Responses are structured and machine-readable
- No questions are lost in conversation history

## Question File Format

### File Naming Convention

Question files MUST follow the naming pattern:
```
{phase-name}-questions.md
```

Place question files in the `.kiro/` directory alongside other project artifacts.

### Question Structure

Each question MUST use the following format with numbered options and an `[Answer]:` tag. The last option MUST always be "Other (please specify)".

Example:
```markdown
## Q1: What is the primary deployment target?
1. AWS Lambda
2. Amazon ECS
3. Amazon EC2
4. Other (please specify)

[Answer]:

## Q2: Which database engine do you prefer?
1. Amazon DynamoDB
2. Amazon Aurora PostgreSQL
3. Amazon RDS MySQL
4. Other (please specify)

[Answer]:
```

The user fills in their choice after `[Answer]:` -- either the option number or free text for "Other".

## Multiple Choice Guidelines

### Option Count

- Minimum: 2 options (including "Other")
- Maximum: 6 options (including "Other")
- Ideal: 3-5 options (including "Other")

If there are more than 5 real choices, group them into categories or split into multiple questions.

### Option Quality

- Options must be mutually exclusive -- no overlapping choices
- Options must be concrete and specific, not vague
- Order options from most common/recommended to least common
- Every question MUST end with "Other (please specify)" as the last option

Good Example:
```markdown
## Q1: What authentication method should be used?
1. Amazon Cognito User Pools
2. IAM-based authentication
3. Third-party OAuth provider (e.g., Auth0, Okta)
4. Other (please specify)

[Answer]:
```

## Workflow Integration

When you need input from the user, follow these four steps in order:

1. **Create** -- Write the question file (`{phase-name}-questions.md`) with all questions formatted per the structure above.
2. **Inform** -- Tell the user the question file has been created, state how many questions it contains, and ask them to fill in the `[Answer]:` fields.
3. **Wait** -- Do NOT proceed until the user confirms they have answered. Never assume or guess answers.
4. **Read** -- Read the completed question file, parse all `[Answer]:` values, and validate them before continuing.

## Error Handling

After reading the question file, validate every answer. Handle the following cases:

### Missing Answers

If any `[Answer]:` tag is empty or missing:
- List the unanswered questions by number.
- Ask the user to complete them in the same question file.
- Wait again before proceeding.

### Invalid Answers

If an answer does not match any provided option number and is not a valid "Other" response:
- Identify the invalid answer and explain why it is invalid.
- Ask the user to correct it in the question file.
- Wait again before proceeding.

### Ambiguous Answers

If an answer is unclear or could map to multiple options:
- State what you interpreted and ask the user to confirm or clarify.
- Handle this via the Contradiction and Ambiguity Detection process below.

## Contradiction and Ambiguity Detection (Modified)

After reading user responses, check for contradictions and ambiguities across all answers in the question file. Look for:
- Answers that conflict with each other (e.g., selecting "serverless" for architecture but "EC2" for deployment)
- Answers that are internally inconsistent with stated requirements
- Answers that are too vague to act on

If contradictions or ambiguities are found:
1. Append a **Clarification** section to the SAME question file -- do NOT create a separate clarification question file.
2. Include 1-2 targeted clarification questions that address the specific contradictions.
3. Inform the user that clarification questions have been added to the existing file.
4. Wait for the user to answer the clarification questions.

Example of appending clarification to an existing question file:
```markdown
---

## Clarification

Your answers to Q1 and Q3 appear to conflict: you selected "serverless" architecture but "EC2" as the compute target. Please clarify:

## C1: Which compute model do you intend?
1. Serverless (Lambda) -- aligning with Q1
2. EC2-based -- aligning with Q3
3. Other (please specify)

[Answer]:
```

## Follow-up Questions (Modified)

One round of follow-up is the maximum. The process is:

1. After reading initial answers, check for contradictions and ambiguities (see above).
2. If clarification is needed, append clarification questions to the same file (one round only).
3. Read the user's clarification answers.
4. If ambiguity remains after this single round of clarification, do the following:
   - State your assumption explicitly and clearly.
   - Document the assumption in the relevant artifact (e.g., design document, spec, or task file).
   - Proceed with work based on that assumption.
   - Do NOT create additional follow-up question files or additional clarification rounds.

This keeps the process lightweight: ask once, clarify once if needed, then move forward.
