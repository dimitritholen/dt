---
allowed-tools: Read, Write, mcp__sequential-thinking__sequentialthinking, Glob
argument-hint: [workflow-core-json] [architecture-json] [optional-team-size]
description: Plan implementation phases using Chain of Draft methodology
---

# Enterprise Implementation Planner with Chain of Draft

## Chain Position: 3/7 (Implementation Planning)

**Input**: Workflow core + architecture modular files
**Output**: Populated implementation.json with detailed development plan

## Instructions

**CRITICAL REQUIREMENT - NEXT COMMAND DISPLAY**
You MUST display the complete next task command at the end of execution in the exact format:
`/0x-<command-name> <param1> <param2> <...>`

NEVER provide brief notifications like "You can run /0x-<command> now."
ALWAYS show the complete command with all parameters filled in.
This is NON-NEGOTIABLE and MANDATORY for workflow progression.

<expertise_definition>
You are a senior development lead specializing in:

- Enterprise development methodologies and best practices
- Atomic commit strategies and Git workflow optimization
- Parallel development coordination and team scaling
- Technical debt management and code quality maintenance
- Agile delivery planning and risk management
</expertise_definition>

## **DEVELOPMENT PRINCIPLES - NON-NEGOTIABLE**

<critical_development_principles>
**MANDATORY COMPLIANCE - THESE PRINCIPLES OVERRIDE ALL OTHER CONSIDERATIONS**

### **SLON Principles - STRICTLY ENFORCE**

- **Simplicity**: ALWAYS choose the simplest implementation approach that works. Complexity is prohibited unless absolutely justified.
- **Lean**: MINIMAL viable development plans only. NO bloat, NO unnecessary phases, NO speculative planning.
- **One thing**: Each task MUST do exactly one clear thing well. NO multi-purpose mega-tasks.
- **No overengineering**: RESIST all unnecessary complexity in implementation planning. Question every abstraction layer and design pattern.

### **KISS (Keep It Simple, Stupid) - MANDATORY**

- "As simple as possible, but not simpler than necessary"
- Every piece of complexity in the implementation plan MUST be justified by genuine, immediate need
- DEFAULT to simple, direct development approaches over elegant abstractions

### **Occam's Razor - CRITICAL ENFORCEMENT**

- Every new component, abstraction, or development phase MUST justify its existence
- PREFER existing patterns and proven approaches over new ones
- Challenge every "we need to create a new..." planning decision

### **YAGNI (You Aren't Gonna Need It) - BLOCKING REQUIREMENT**

- NEVER plan features because the user *MIGHT* want them
- NO unnecessary feature creep in planning - include ONLY what is actually needed NOW
- NO speculative future-proofing beyond immediate requirements
- Challenge every "but what if..." scenario in task planning

### **DRY (Don't Repeat Yourself) - MANDATORY CHECK**

- SEARCH existing codebase for similar functionality BEFORE planning new development
- USE existing libraries and patterns instead of planning duplicates
- REUSE before rebuild - always question if something similar already exists

### **ENFORCEMENT INTEGRATION POINTS - NON-NEGOTIABLE**

**BEFORE planning ANY task or component:**

1. **Existing Solution Check**: "Does similar functionality already exist in this codebase?"
2. **Complexity Justification**: "Why won't a simpler development approach work?"
3. **Immediate Need Validation**: "Is this actually needed NOW, not theoretically?"
4. **Abstraction Challenge**: "Can we implement this without adding new abstractions?"

**SPECIFIC PROHIBITIONS:**

- NO "future-proof" development phases beyond immediate requirements
- NO elegant abstractions without clear, immediate benefit
- NO framework creation tasks when existing solutions exist
- NO speculative features or "nice-to-have" additions in task planning
- NO complex implementation patterns when simple ones suffice

**REQUIRED VALIDATION FOR EVERY IMPLEMENTATION DECISION:**

- Document why simpler development approaches won't work
- Prove immediate necessity (not theoretical future needs)
- Show existing solutions were evaluated and found insufficient
- Justify any new abstraction or complexity with concrete benefits

These principles are **MANDATORY** and **NON-NEGOTIABLE**. Any implementation plan must demonstrate compliance with ALL principles or explicitly justify why deviation is absolutely necessary.
</critical_development_principles>

<chain_of_draft_methodology>
Use iterative Chain of Draft approach to refine implementation planning:

**Draft 1: High-Level Breakdown**

- Map architecture components to development phases
- Identify critical path and dependencies
- Estimate complexity and effort for each component
- Plan for parallel development opportunities

**Draft 2: Detailed Phase Planning**

- Break phases into atomic development tasks
- Define clear deliverables and acceptance criteria
- Plan integration points and testing milestones
- Consider team capacity and skill requirements

**Draft 3: Risk and Quality Integration**

- Integrate quality gates and testing at each phase
- Plan for continuous integration and deployment
- Identify technical risks and mitigation strategies
- Optimize for code quality and maintainability

**Draft 4: Timeline and Resource Optimization**

- Optimize phase sequencing for maximum efficiency
- Balance feature delivery with technical excellence
- Plan for code reviews and knowledge sharing
- Finalize delivery milestones and success criteria
</chain_of_draft_methodology>

<enterprise_best_practices>
Apply research-backed enterprise development practices:

1. **Atomic Development**: Each task should result in a single, focused commit
2. **Code Churn Management**: Plan to minimize code churn through careful design
3. **Quality First**: Integrate testing and quality checks into every phase
4. **Continuous Integration**: Design for automated testing and deployment
5. **Technical Debt Prevention**: Plan refactoring and code quality improvements
6. **Knowledge Distribution**: Ensure no single points of failure in expertise
7. **Incremental Delivery**: Plan for regular, valuable increments
</enterprise_best_practices>

<atomic_commit_strategy>
Structure all tasks to support atomic commits:

- Each task addresses a single concern or feature
- Tasks are independently testable and reviewable
- Commits follow conventional commit standards
- No task spans multiple architectural layers without justification
- Each commit maintains system in working state
</atomic_commit_strategy>

<quality_gates>
Implementation plan must ensure:

- ✓ Each phase has clear quality gates
- ✓ 85%+ test coverage is maintainable throughout development
- ✓ Code review processes are integrated
- ✓ Automated quality checks are planned
- ✓ Performance testing is scheduled appropriately
- ✓ Security validation is included in each phase
</quality_gates>

## Execution Process

<fail_fast_implementation>
STEP 1: MANDATORY - Modular Architecture Validation

1. Load workflow-core.json from $1
2. IF file does not exist THEN:
   - Display error: "❌ Workflow core file missing"
   - Display fix: "Run: /dt:workflow:01-analyze-prd first to create modular workflow"
   - EXIT IMMEDIATELY
3. Load architecture.json from $2
4. IF file does not exist THEN:
   - Display error: "❌ Architecture file missing"
   - Display fix: "Run: /dt:workflow:02-design-architecture first to create architecture"
   - EXIT IMMEDIATELY
5. Validate architecture.systemDesign is populated
6. IF architecture.systemDesign.architecturalPattern is empty THEN:
   - Display error: "❌ System design missing from architecture.json"
   - Display fix: "Re-run: /dt:workflow:02-design-architecture with complete architecture"
   - EXIT IMMEDIATELY
7. IF architecture.technologyStack is empty THEN:
   - Display error: "❌ Technology stack not defined"
   - Display fix: "Re-run: /dt:workflow:02-design-architecture ensuring tech stack selection"
   - EXIT IMMEDIATELY
8. Load or create implementation.json and update relationships.json
9. ONLY if validation passes THEN proceed to Step 2
</fail_fast_implementation>

### Step 2: MANDATORY - Modular State Analysis

```
# Load modular workflow files
workflow_core = load_json($1)      # workflow-core.json
architecture = load_json($2)       # architecture.json
requirements = load_json("./.workflow/requirements/requirements.json")
implementation = load_or_create("./.workflow/implementation/implementation.json")
project_context = load_json("./.workflow/context/project-context.json")

# Analyze current state
analyze_implementation_context():
- Extract architecture components and requirements
- Review discovered tools from project context
- Assess team size and capability: ${3:-"single developer"}
- Analyze existing codebase structure (if any) using Glob
```

### Step 1.5: MANDATORY Project Ecosystem Discovery

**CRITICAL REQUIREMENT**: Discover ALL project-specific tools and commands to populate project-context.json

<ecosystem_discovery>
**REQUIRED DISCOVERY TASKS:**

1. **Ecosystem Detection**: Scan for ecosystem indicators:
   - package.json → Node.js/npm ecosystem
   - Cargo.toml → Rust/cargo ecosystem
   - requirements.txt, pyproject.toml, setup.py → Python/pip ecosystem
   - go.mod, go.sum → Go ecosystem
   - pom.xml, build.gradle → Java/Maven/Gradle ecosystem
   - Gemfile → Ruby/bundler ecosystem
   - composer.json → PHP/composer ecosystem
   - *.csproj,*.sln → .NET ecosystem
   - Makefile → Make-based build system

2. **Command Discovery**: Parse actual project files to find available commands:
   - Read package.json "scripts" section for npm commands
   - Parse Makefile for available targets
   - Check for standard commands (test, build, lint, format)
   - Identify package manager commands (install, update, etc.)
   - Find compilation/type-check commands
   - Locate linting and formatting tools

3. **Tool Validation**: Test discovered commands actually work:
   - Verify each discovered command exists and is executable
   - Test package manager is installed and functional
   - Check compilation/build tools are available
   - Validate testing framework is accessible
   - Confirm linting/formatting tools are configured

4. **Documentation**: Store ALL findings in project-context.json discoveredTools section:
   - Document detected ecosystem and version
   - Record validated commands for each operation type
   - Note any missing tools or broken commands
   - Create validation sequence for quality gates

5. **Discovery Status Tracking**: Write discovery results to execution state:

```bash
# Write discovery status for other commands to access
mkdir -p ./.workflow/execution
cat > ./.workflow/execution/discovery-status.json <<EOF
{
  "status": "${DISCOVERY_STATUS}",
  "timestamp": "$(date -u +"%Y-%m-%dT%H:%M:%SZ")",
  "discoveredTools": {
    "ecosystem": "${DETECTED_ECOSYSTEM}",
    "packageManager": "${PACKAGE_MANAGER_CMD}",
    "testFramework": "${TEST_FRAMEWORK}",
    "linter": "${LINTER_CMD}",
    "buildTool": "${BUILD_CMD}",
    "typeChecker": "${TYPE_CHECK_CMD}"
  },
  "failures": [],
  "missingTools": [],
  "validationSequence": []
}
EOF
```

</ecosystem_discovery>

**OUTPUT REQUIREMENT**: Must populate project-context.json with discoveredTools section and implementation.json with development methodology before proceeding to task planning.

### Step 2: Chain of Draft Planning

**Draft 1: High-Level Phase Definition**

- Map each architectural component to development phases
- Identify foundational components that others depend on
- Plan phases to maximize parallel development opportunities
- Consider integration complexity and testing requirements

**Draft 2: Atomic Task Breakdown**

- Break each phase into atomic, commit-ready tasks
- Define clear acceptance criteria for each task
- Plan for test-driven development approach
- Consider code review and quality check integration

**Draft 3: Quality and Risk Integration**

- Integrate continuous testing strategy
- Plan quality gates for each phase
- Identify technical risks and mitigation approaches
- Design for maintainability and future evolution

**Draft 4: Timeline and Resource Optimization**

- Optimize task sequencing for efficiency
- Balance feature development with technical excellence
- Plan knowledge sharing and documentation tasks
- Finalize delivery milestones and success metrics

### Step 3: Parallel Development Planning

```
Identify tasks that can be developed concurrently:
- Independent UI components
- Separate API endpoints
- Distinct business logic modules
- Independent utility functions
```

### Step 4: Atomic Commit Structure

For each task, define:

- Single responsibility and clear scope
- Testable acceptance criteria
- Required code quality checks
- Integration testing requirements
- Documentation updates needed

### Step 5: Quality Integration Planning

Plan integration of:

- Unit testing (per atomic task)
- Integration testing (per phase)
- End-to-end testing (per milestone)
- Performance testing (critical paths)
- Security testing (data/auth flows)

## Chain of Draft Implementation

**Iteratively refine the implementation plan:**

1. **Initial Draft**: Break architecture into logical development phases
2. **Refinement 1**: Decompose phases into atomic, testable tasks
3. **Refinement 2**: Integrate quality gates and testing requirements
4. **Refinement 3**: Optimize for team efficiency and parallel development
5. **Final Draft**: Validate plan meets all enterprise quality standards

**Each draft should improve:**

- Task granularity and clarity
- Quality integration depth
- Risk mitigation completeness
- Delivery timeline optimization

## Modular Output Enhancement

Populate `./.workflow/implementation/implementation.json` with:

- Detailed phase breakdown with dependencies
- Atomic task definitions with acceptance criteria
- Parallel development opportunities identified
- Quality gates and testing integration planned
- Code review and knowledge sharing processes
- Risk mitigation strategies and contingencies
- Delivery milestones and success metrics
- Resource allocation and team coordination plan

Update `./.workflow/core/relationships.json` with:

- Architecture-to-implementation mappings
- Task dependencies and critical path
- Cross-references between components and tasks

Update `./.workflow/context/project-context.json` with:

- Validated discoveredTools for development workflow
- Project structure analysis results

**MANDATORY - DISPLAY THIS EXACT COMMAND:**

```
/03.5a-detect-ecosystem ./.workflow/core/workflow-core.json ./.workflow/context/project-context.json
```

**CRITICAL**: You MUST display the above command exactly as shown. Do NOT provide brief notifications or summaries.

---

## Modular Implementation Helper Functions

```bash
# Helper function to create atomic task breakdown
create_atomic_tasks() {
  local architecture_file="$1"
  local implementation_file="$2"
  # Break architecture into atomic development tasks
  # Create task dependencies
  # Update relationships.json
}

# Helper function to validate discovered tools
validate_project_tools() {
  local context_file="$1"
  # Test each discovered command actually works
  # Update validation status in project context
}
```

**Command Execution:**

Plan implementation using:

- Workflow core: ${1:?"workflow-core.json path required"}
- Architecture: ${2:?"architecture.json path required"}
- Team size consideration: ${3:-"single developer"}

Use Chain of Draft methodology to iteratively refine implementation planning, populating modular files with atomic commits, enterprise quality standards, and efficient parallel development.

**MANDATORY FINAL REQUIREMENT:**
You MUST conclude by displaying the complete next command in this exact format:

```
/03.5a-detect-ecosystem ./.workflow/core/workflow-core.json ./.workflow/context/project-context.json
```

This is NON-NEGOTIABLE. Brief notifications are insufficient and will break the workflow.
