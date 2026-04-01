# Build and Test

**Purpose**: Build all units and execute comprehensive testing strategy

## Prerequisites
- Code Generation must be complete for all units
- All code artifacts must be generated
- Project is ready for build and testing

---

## Step 1: Analyze Testing Requirements

Analyze the project to determine appropriate testing strategy:
- **Unit tests**: Already generated per unit during code generation
- **Integration tests**: Test interactions between units/services
- **Performance tests**: Only if performance NFRs exist
- **End-to-end tests**: Only if end-to-end user workflows need validation
- **Contract tests**: Only for microservices with API contracts
- **Security tests**: Only if security requirements are specified

---

## Step 2: Generate Build and Test Instructions

Create `aidlc-docs/construction/build-and-test/build-and-test-instructions.md` combining build, unit test, and integration test instructions into a single file. Include:

**Build section**:
- Build prerequisites (tool, dependencies, env vars, system requirements)
- Build steps (install dependencies, configure environment, build all units)
- Verify build success (expected output, build artifacts)
- Troubleshooting (dependency errors, compilation errors)

**Unit Test section**:
- Command to run all unit tests
- Expected results (pass count, coverage percentage, report location)
- Steps to fix failing tests

**Integration Test section**:
- Purpose and test scenarios (unit-to-unit interactions)
- Setup instructions (start services, configure endpoints)
- Run commands and verification steps
- Cleanup commands

---

## Step 3: Generate Additional Test Instructions (Conditional)

Only generate these files when explicitly relevant to the project. Each goes in `aidlc-docs/construction/build-and-test/`:

- **Performance tests** (`performance-test-instructions.md`): Only if performance NFRs exist. Include load test setup, test parameters, execution commands, and results analysis.
- **Contract tests** (`contract-test-instructions.md`): Only for microservices with API contracts. Include consumer-driven contract testing and schema validation.
- **Security tests** (`security-test-instructions.md`): Only if security requirements are specified. Include vulnerability scanning, dependency checks, and auth testing.
- **E2E tests** (`e2e-test-instructions.md`): Only if end-to-end user workflows need validation. Include complete user workflow testing and cross-service scenarios.

---

## Step 4: Generate Test Summary

Create `aidlc-docs/construction/build-and-test/build-and-test-summary.md` containing:
- **Build Status**: tool, status, artifacts, build time
- **Unit Tests**: total, passed, failed, coverage, status
- **Integration Tests**: scenarios, passed, failed, status
- **Additional Tests**: performance/contract/security/e2e (Pass/Fail/N/A each)
- **Overall Status**: build result, all tests result, ready for operations (Yes/No)
- **Next Steps**: proceed to Operations if all pass, or address failures and rebuild

---

## Step 5: Update State Tracking

Update `aidlc-docs/aidlc-state.md`:
- Mark Build and Test stage as complete
- Update current status

---

## Step 6: Present Results to User

Present comprehensive message:

```
"Build and Test Complete!

**Build Status**: [Success/Failed]

**Test Results**:
- Unit Tests: [X] passed
- Integration Tests: [X] scenarios passed
- Performance Tests: [Status or N/A]
- Additional Tests: [Status or N/A]

**Generated Files**:
1. build-and-test-instructions.md
2. [conditional test files as applicable]
3. build-and-test-summary.md

Review the summary in aidlc-docs/construction/build-and-test/build-and-test-summary.md

**Ready to proceed to Operations stage for deployment planning?**"
```

---

## Step 7: Log Interaction

**MANDATORY**: Log the phase completion in `aidlc-docs/audit.md`:

```markdown
## Build and Test Stage
**Timestamp**: [ISO timestamp]
**Build Status**: [Success/Failed]
**Test Status**: [Pass/Fail]
**Files Generated**:
- build-and-test-instructions.md
- [conditional test instruction files]
- build-and-test-summary.md
```
