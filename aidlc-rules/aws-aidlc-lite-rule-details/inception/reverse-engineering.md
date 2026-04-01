# Reverse Engineering

**Purpose**: Analyze existing codebase and generate comprehensive design artifacts

**Execute when**: Brownfield project detected (existing code found in workspace)

**Skip when**: Greenfield project (no existing code)

**Rerun behavior**: Always rerun when brownfield project detected, even if artifacts exist. This ensures artifacts reflect current code state

## Step 1: Multi-Package Discovery

### 1.1 Scan Workspace
- All packages (not just mentioned ones)
- Package relationships via config files
- Package types: Application, CDK/Infrastructure, Models, Clients, Tests

### 1.2 Understand the Business Context
- The core business that the system is implementing overall
- The business overview of every package
- List of Business Transactions that are implemented in the system

### 1.3 Infrastructure Discovery
- CDK packages (package.json with CDK dependencies)
- Terraform (.tf files)
- CloudFormation (.yaml/.json templates)
- Deployment scripts

### 1.4 Build System Discovery
- Build systems: Brazil, Maven, Gradle, npm
- Config files for build-system declarations
- Build dependencies between packages

### 1.5 Service Architecture Discovery
- Lambda functions (handlers, triggers)
- Container services (Docker/ECS configs)
- API definitions (Smithy models, OpenAPI specs)
- Data stores (DynamoDB, S3, etc.)

### 1.6 Code Quality Analysis
- Programming languages and frameworks
- Test coverage indicators
- Linting configurations
- CI/CD pipelines

## Step 2: Generate System Overview Documentation

Create `aidlc-docs/inception/reverse-engineering/system-overview.md` containing:

**Business Context:**
- Business Description (overall system purpose)
- Business Transactions (list with descriptions)
- Business Dictionary (key terms and meanings)
- Component-level business descriptions (purpose and responsibilities per package)

**System Architecture:**
- System overview and architecture diagram (Mermaid)
- Component descriptions (purpose, responsibilities, dependencies, type per package)
- Data flow (Mermaid sequence diagram of key workflows)
- Integration points (external APIs, databases, third-party services)
- Infrastructure components (CDK stacks, deployment model, networking)

**Code Structure:**
- Build system type and configuration
- Key classes/modules (Mermaid class diagram or module hierarchy)
- Existing files inventory (path and purpose for each source file)
- Design patterns (name, location, purpose, implementation)
- Critical dependencies (name, version, usage, purpose)

**Component Inventory:**
- Application packages (name, purpose)
- Infrastructure packages (name, CDK/Terraform, purpose)
- Shared packages (name, Models/Utilities/Clients, purpose)
- Test packages (name, Integration/Load/Unit, purpose)
- Total counts (overall, application, infrastructure, shared, test)

**Technology Stack:**
- Programming languages (language, version, usage)
- Frameworks (framework, version, purpose)
- Infrastructure (service, purpose)
- Build tools (tool, version, purpose)
- Testing tools (tool, version, purpose)

## Step 3: Generate API and Dependencies Documentation

Create `aidlc-docs/inception/reverse-engineering/api-and-dependencies.md` containing:

**REST APIs:**
- Endpoint name, method (GET/POST/PUT/DELETE), path, purpose, request format, response format

**Internal APIs:**
- Interface/class name, methods with signatures, parameters, return types

**Data Models:**
- Model name, fields, relationships, validation rules

**Internal Dependencies:**
- Package dependency diagram (Mermaid)
- For each dependency: type (Compile/Runtime/Test), reason

**External Dependencies:**
- Dependency name, version, purpose, license type

## Step 4: Update State Tracking

Update `aidlc-docs/aidlc-state.md`:

```markdown
## Reverse Engineering Status
- [x] Reverse Engineering - Completed on [timestamp]
- **Artifacts Location**: aidlc-docs/inception/reverse-engineering/
```

## Step 5: Present Completion Message

```markdown
# Reverse Engineering Complete

[AI-generated summary of key findings from analysis in bullet points]

> **REVIEW REQUIRED:**
> Please examine the reverse engineering artifacts at: `aidlc-docs/inception/reverse-engineering/`

> **WHAT'S NEXT?**
>
> **You may:**
>
> **Request Changes** - Ask for modifications to the reverse engineering analysis if required
> **Approve & Continue** - Approve analysis and proceed to **Requirements Analysis**
```

## Step 6: Wait for User Approval

- **MANDATORY**: Do not proceed until user explicitly approves
- **MANDATORY**: Log user's response in audit.md with complete raw input
