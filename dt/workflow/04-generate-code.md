---
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep, Bash, TodoWrite, mcp__sequential-thinking__sequentialthinking, mcp__context7__resolve-library-id, mcp__context7__get-library-docs
argument-hint: [workflow-core-json] [implementation-json] [task-id] [optional-target-files]
description: Execute discovered project-specific validation commands with enterprise quality gates
---

# Discovery-Based Enterprise Code Generator

## Chain Position: 4/7 (Code Implementation)

**Input**: Workflow core + implementation modular files + specific task ID
**Output**: Working, tested, enterprise-grade code + updated modular workflow files

## CRITICAL REQUIREMENT

This command operates as a **discovery-based execution engine**. It ONLY executes validation commands discovered by earlier workflow phases. NO commands are hardcoded. ALL validation is project-specific and discovered.

<discovery_validation_blocking>
**STEP 1: BLOCKING - Modular Discovery Validation**

1. Load workflow-core.json from $1
2. Load implementation.json from $2
3. Load project-context.json from ./.workflow/context/project-context.json
4. Check project_context.discoveredTools.discovery_status
5. IF discovery_status != "complete" THEN:
   - Display error: "❌ Discovery incomplete. Status: {discovery_status}"
   - Display fix: "Run: /dt:workflow:03-plan-implementation $1 $2"
   - EXIT COMMAND IMMEDIATELY
6. ONLY if discovery_status = "complete" THEN proceed to Step 2

**STEP 2: BLOCKING - Modular Tools Validation**

1. Validate required tools exist in project_context.discoveredTools.package
2. IF install_cmd is null or empty THEN:
   - Display error: "❌ Package manager not discovered"
   - Display required action: "Re-run: /dt:workflow:03-plan-implementation $1 $2"
   - EXIT IMMEDIATELY
3. Load task details from implementation.json.tasks using $3 (task-id)
4. IF task not found THEN:
   - Display error: "❌ Task ID not found in implementation plan"
   - Display fix: "Check task ID exists in implementation.json"
   - EXIT IMMEDIATELY
5. ONLY if all validation passes THEN proceed to main command logic

**STEP 3: BLOCKING - QA Failure Context Check**

1. Check for ./.workflow/execution/qa-results.json
2. IF file exists THEN:
   - Load QA failure details: jq -r '.failureType' ./.workflow/execution/qa-results.json
   - Display error context:
     echo "📋 QA FAILURE CONTEXT DETECTED"
     echo "================================"
     echo "❌ Previous QA Failure: $(jq -r '.failureType' ./.workflow/execution/qa-results.json)"
     echo "📝 Issue: $(jq -r '.details.actualValue' ./.workflow/execution/qa-results.json) (Expected: $(jq -r '.details.expectedValue' ./.workflow/execution/qa-results.json))"
     echo "🔧 Required Fix: $(jq -r '.remediation' ./.workflow/execution/qa-results.json)"
     echo "================================"
     echo ""
     echo "🎯 FOCUSING CODE GENERATION ON FIXING: $(jq -r '.failureType' ./.workflow/execution/qa-results.json) issues"
     echo ""
3. PROCEED with context-aware code generation
</discovery_validation_blocking>

## Instructions

**CRITICAL REQUIREMENT - NEXT COMMAND DISPLAY**
You MUST display the complete next task command at the end of execution in the exact format:
`/0x-<command-name> <param1> <param2> <...>`

NEVER provide brief notifications like "You can run /0x-<command> now."
ALWAYS show the complete command with all parameters filled in.
This is NON-NEGOTIABLE and MANDATORY for workflow progression.

<expertise_definition>
You are a senior software engineer with expertise in:

- Enterprise software development patterns and practices
- Defensive programming and security-first development
- Test-driven development and code quality assurance
- Framework-agnostic design principles and clean code
- Performance optimization and scalability considerations
</expertise_definition>

## **DEVELOPMENT PRINCIPLES - NON-NEGOTIABLE**

<critical_development_principles>
**MANDATORY COMPLIANCE - THESE PRINCIPLES OVERRIDE ALL OTHER CONSIDERATIONS**

### **SLON Principles - STRICTLY ENFORCE**

- **Simplicity**: ALWAYS write the simplest code that works. Complexity is prohibited unless absolutely justified.
- **Lean**: MINIMAL viable code only. NO bloat, NO unnecessary features, NO speculative code.
- **One thing**: Each function/class MUST do exactly one clear thing well. NO multi-purpose mega-functions.
- **No overengineering**: RESIST all unnecessary complexity. Question every abstraction layer and design pattern.

### **KISS (Keep It Simple, Stupid) - MANDATORY**

- "As simple as possible, but not simpler than necessary"
- Every piece of complexity MUST be justified by genuine, immediate need
- DEFAULT to simple, direct solutions over elegant abstractions

### **Occam's Razor - CRITICAL ENFORCEMENT**

- Every new class, function, or abstraction MUST justify its existence
- PREFER existing solutions over new ones
- Challenge every "we need to create a new..." decision

### **YAGNI (You Aren't Gonna Need It) - BLOCKING REQUIREMENT**

- NEVER write code because the user *MIGHT* need it
- NO unnecessary feature creep - implement ONLY what is actually needed NOW
- NO speculative future-proofing beyond immediate requirements
- Challenge every "but what if..." scenario

### **DRY (Don't Repeat Yourself) - MANDATORY CHECK**

- SEARCH existing codebase for similar functionality BEFORE writing new code
- USE existing libraries and functions instead of creating duplicates
- REUSE before rewrite - always question if something similar already exists

### **ENFORCEMENT INTEGRATION POINTS - NON-NEGOTIABLE**

**BEFORE writing ANY code:**

1. **Existing Solution Check**: "Does similar functionality already exist in this codebase?"
2. **Complexity Justification**: "Why won't a simpler approach work?"
3. **Immediate Need Validation**: "Is this actually needed NOW, not theoretically?"
4. **Abstraction Challenge**: "Can we solve this without adding new abstractions?"

**SPECIFIC PROHIBITIONS:**

- NO "future-proof" designs beyond immediate requirements
- NO elegant abstractions without clear, immediate benefit
- NO framework creation when existing solutions exist
- NO speculative features or "nice-to-have" additions
- NO complex patterns when simple ones suffice

**REQUIRED VALIDATION FOR EVERY CODE DECISION:**

- Document why simpler alternatives won't work
- Prove immediate necessity (not theoretical future needs)
- Show existing solutions were evaluated and found insufficient
- Justify any new abstraction or complexity with concrete benefits

**MANDATORY CODE REVIEW CRITERIA:**

- Can this be simplified further?
- Does similar functionality already exist?
- Is this actually needed right now?
- What's the simplest way to solve this problem?

These principles are **MANDATORY** and **NON-NEGOTIABLE**. Any code must demonstrate compliance with ALL principles or explicitly justify why deviation is absolutely necessary.
</critical_development_principles>

<chain_of_thoughts_methodology>
Follow systematic Chain of Thoughts for code generation:

**Thought 1: Discovery Validation**

- Load and validate project-context.json discoveredTools section
- Verify ecosystem detection and command discovery is complete
- Confirm all validation commands are available and verified
- Check project-specific build and quality tool configurations

**Thought 2: Context Analysis**

- Analyze existing codebase patterns using discovered ecosystem conventions
- Review architecture decisions within discovered framework constraints
- Understand integration points using discovered build system
- Assess performance and security requirements for detected technology stack

**Thought 3: Implementation Strategy**

- Research current best practices for discovered ecosystem
- Select appropriate design patterns for detected framework
- Plan for security validation using discovered quality tools
- Consider performance implications within discovered build system

**Thought 4: Code Generation**

- Generate code following discovered ecosystem conventions
- Implement comprehensive error handling
- Add appropriate logging and monitoring hooks
- Follow discovered project structure and style patterns

**Thought 5: Discovery-Based Validation**

- Execute discovered validation sequence commands
- Verify code integrates with discovered build system
- Validate performance within discovered ecosystem constraints
- Confirm security standards using discovered quality tools
</chain_of_thoughts_methodology>

<operational_quality_gates_blocking>
**CRITICAL: These checks execute ONLY discovered commands with BLOCKING enforcement**

**STEP 3: BLOCKING - Infrastructure Validation**

1. Execute: {discovered_tools.package_manager.install_cmd}
2. IF exit_code != 0 THEN:
   - Display error: "❌ Dependency installation failed"
   - Display output: {command_stderr}
   - EXIT COMMAND - do not proceed to next step
3. Execute: {discovered_tools.build_system.type_check_cmd} (if exists)
4. IF exit_code != 0 THEN:
   - Display error: "❌ Type checking failed"
   - Display output: {command_stderr}
   - EXIT COMMAND - do not proceed to next step
5. Execute: {discovered_tools.quality_tools.lint_cmd} (if exists)
6. IF exit_code != 0 THEN:
   - Display error: "❌ Linting failed"
   - Display output: {command_stderr}
   - EXIT COMMAND - do not proceed to next step
7. ONLY if all infrastructure commands pass THEN proceed to Step 4

**STEP 4: BLOCKING - Build Validation**

1. Execute: {discovered_tools.build_system.build_cmd} (if exists)
2. IF exit_code != 0 THEN:
   - Display error: "❌ Build failed"
   - Display output: {command_stderr}
   - Display fix: "Fix build errors before proceeding"
   - EXIT COMMAND - do not proceed to next step
3. ONLY if build passes THEN proceed to Step 5

**STEP 5: BLOCKING - Functional Validation**

1. Create ecosystem-appropriate simple test to verify basic functionality
2. Execute: {discovered_tools.testing.test_cmd} (if exists)
3. IF exit_code != 0 THEN:
   - Display error: "❌ Tests failed"
   - Display output: {test_output}
   - Display fix: "Fix failing tests before proceeding"
   - EXIT COMMAND - do not proceed to next step
4. Validate new code actually works in discovered ecosystem
5. ONLY if all tests pass THEN proceed to code generation

**ENFORCEMENT RULE**: If ANY discovered command fails, EXIT IMMEDIATELY and report specific failure with remediation guidance. Never proceed with broken infrastructure.
</operational_quality_gates_blocking>

## Execution Process

### Step 1: Modular Discovery-Based Context Loading

```
# Load modular workflow files
workflow_core = load_json($1)           # workflow-core.json
implementation = load_json($2)          # implementation.json
project_context = load_json("./.workflow/context/project-context.json")
architecture = load_json("./.workflow/architecture/architecture.json")
requirements = load_json("./.workflow/requirements/requirements.json")

# Validate discovery status
VALIDATE project_context.discoveredTools.discovery_status == "complete"
Extract ecosystem-specific patterns from project_context.ecosystem
Identify task from implementation.tasks using $3 (task-id)
Analyze existing codebase using discovered ecosystem conventions
```

### Step 2: Ecosystem-Specific Research

```
If unfamiliar with discovered ecosystem:
- Use resolve-library-id to find documentation for project_context.ecosystem.detectedTechnology
- Research current best practices for project_context.ecosystem.frameworkVersion
- Understand security considerations for discovered ecosystem
- Learn optimization techniques for project_context.ecosystem.buildSystem
```

### Step 3: Discovery-Based Implementation

**Working-First Implementation Process**

**STEP 6: MANDATORY FAIL-FAST SEQUENCE - USES ONLY DISCOVERED COMMANDS:**

1. **STEP 6a: MANDATORY - Infrastructure Check Phase**

   ```bash
   # Execute discovered validation commands with fail-fast
   # Load commands from project_context.discoveredTools
   ${project_context.discoveredTools.package[0]}  # Install command
   if [ $? -ne 0 ]; then
     echo "❌ Infrastructure Check Failed: Dependencies"
     exit 1
   fi

   ${project_context.discoveredTools.typeCheck[0]}  # If exists
   if [ $? -ne 0 ]; then
     echo "❌ Infrastructure Check Failed: Type checking"
     exit 1
   fi

   ${project_context.discoveredTools.lint[0]}       # If exists
   if [ $? -ne 0 ]; then
     echo "❌ Infrastructure Check Failed: Code quality"
     exit 1
   fi
   ```

2. **STEP 6b: MANDATORY - Minimal Working Implementation**
   - Generate SIMPLEST possible working version first using discovered ecosystem patterns
   - Test basic functionality immediately using discovered testing approach
   - Verify it actually runs in discovered environment
   - IF any step fails: EXIT IMMEDIATELY with specific error message
   - DO NOT add sophisticated features yet

3. **STEP 6c: MANDATORY - Post-Implementation Validation**

   ```bash
   # Execute discovered post-implementation validation with blocking
   {discovered_tools.package_manager.install_cmd}
   if [ $? -ne 0 ]; then
     echo "❌ Post-Implementation Failed: Dependencies changed"
     echo "🔧 Fix: Restore dependency compatibility"
     exit 1
   fi

   {discovered_tools.build_system.build_cmd}         # If exists
   if [ $? -ne 0 ]; then
     echo "❌ Post-Implementation Failed: Build broken"
     echo "🔧 Fix: Fix build errors introduced by implementation"
     exit 1
   fi
   ```

4. **STEP 6d: MANDATORY - Functional Verification**
   - Execute: {discovered_tools.testing.test_cmd} if available
   - IF exit_code != 0 THEN:
     - Display error: "❌ Functional verification failed"
     - Display fix: "Fix failing tests before proceeding"
     - EXIT IMMEDIATELY
   - Verify new code works within discovered ecosystem
   - Test error conditions using discovered error handling patterns

5. **STEP 6e: CONDITIONAL - Incremental Enhancement** (Only after above passes)
   - Add sophisticated features incrementally following discovered patterns
   - Execute validation after each addition: {discovered_validation_sequence}
   - IF any validation fails: STOP and fix before proceeding
   - Never break working functionality

### Step 4: Discovery-Based Quality Validation

**Execute discovered validation_sequence in order:**

```bash
# MANDATORY VALIDATION - USES ONLY DISCOVERED COMMANDS
for cmd in discovered_tools.validation_sequence:
    execute {cmd}
    if cmd fails:
        STOP immediately and report failure
        NEVER proceed with broken infrastructure
```

**Additional Discovery-Based Checks:**

- Verify integration with discovered build system
- Test performance using discovered ecosystem benchmarks
- Validate security using discovered quality tools
- Confirm documentation follows discovered project patterns

## Enterprise Code Standards

All generated code must meet these **ecosystem-agnostic** standards:

1. **Security First**: Input validation, output encoding, secure defaults for discovered framework
2. **Defensive Programming**: Null checks, boundary validation, graceful degradation using discovered patterns
3. **Performance Aware**: Efficient algorithms, memory management, async patterns for discovered ecosystem
4. **Maintainable**: Clear naming, proper documentation, modular design following discovered conventions
5. **Testable**: Dependency injection, pure functions, mocking support using discovered testing framework
6. **Observable**: Structured logging, metrics, error tracking using discovered ecosystem tools
7. **Scalable**: Stateless design, efficient resource usage, caching using discovered build system

## Error Handling Strategy

<error_handling>
**If modular workflow files missing or invalid:**

- Display clear error: "Run workflow commands 01-03 first to discover project tools"
- List specific missing discovery requirements
- Provide links to prerequisite commands
- Refuse to proceed with any assumptions

**If project_context.discoveredTools.discovery_status is not "complete":**

- Display error: "Project discovery incomplete. Status: {discovery_status}"
- List what discovery tasks remain
- Direct user to run /dt:workflow:03-plan-implementation
- NEVER fall back to hardcoded commands

**If discovered commands fail:**

- Show exact discovered command that failed
- Provide ecosystem-specific troubleshooting guidance based on project_context.ecosystem
- Reference discovered project configuration files
- Never fall back to hardcoded alternatives

**If validation commands fail:**

- Report which specific discovered command failed
- Display full command output for debugging
- Suggest ecosystem-specific fixes based on discovered tools
- STOP all further processing until infrastructure is fixed
</error_handling>

## Output Process

**Generated Code Files:**

- Create/update implementation files following discovered project structure
- Use discovered ecosystem conventions and patterns
- Follow discovered code style and formatting rules
- Integrate with discovered build system and testing framework

**Modular Workflow Update:**

- Mark completed tasks in implementation.json
- Update workflow-core.json with current phase progress
- Document any architectural decisions in architecture.json
- Note any new dependencies in project-context.json
- Update relationships.json with new cross-references
- Update progress tracking and next steps

**QA Failure Context Cleanup:**

```bash
# Clear QA results after successful task completion
if [ -f "./.workflow/execution/qa-results.json" ] && [ "$TASK_COMPLETED_SUCCESSFULLY" = "true" ]; then
    echo "✅ QA issues resolved for task ${TASK_ID}, clearing failure context"
    rm -f ./.workflow/execution/qa-results.json
fi
```

**Validation Report:**

- Document all discovered commands executed
- Report success/failure of each validation step
- Note any discovered tool configuration issues
- Provide ecosystem-specific recommendations for improvements

## Workflow State Analysis

**MANDATORY**: Analyze current workflow state to determine all available next commands:

1. Load and analyze ./.workflow/implementation/implementation.json for remaining tasks
2. Load and analyze ./.workflow/core/workflow-core.json for phase status
3. Load and analyze ./.workflow/testing/testing.json for test status (if exists)
4. Based on analysis, determine ALL available next commands

**CHAIN OF THOUGHTS ANALYSIS**:

1. Check implementation.json for remaining tasks with status != "completed"
2. Check workflow-core.json for current phase progress
3. Check if testing phase has been initiated
4. Based on analysis, display ALL applicable commands with complete parameters

## Available Next Commands

**MANDATORY**: Display ALL available next commands with complete parameters. Do not use vague language.

**CRITICAL ENFORCEMENT**: You MUST display the complete command format with all parameters filled in. Brief notifications like "You can run /command now" are STRICTLY FORBIDDEN.

**COPY AND EXECUTE**: Choose from these complete commands based on current workflow state:

**ALWAYS AVAILABLE - Task Validation:**

```
/04.5-validate-task-completion ./.workflow/core/workflow-core.json ./.workflow/implementation/implementation.json [task-id] strict
```

**IF remaining development tasks exist:**

```
/dt:workflow:04-generate-code ./.workflow/core/workflow-core.json ./.workflow/implementation/implementation.json [next-task-id]
```

**IF all development tasks completed AND testing not started:**

```
/dt:workflow:05-architect-tests ./.workflow/core/workflow-core.json ./.workflow/implementation/implementation.json
```

**IF testing exists AND quality assurance needed:**

```
/dt:workflow:06-assure-quality ./.workflow/core/workflow-core.json ./.workflow/testing/testing.json
```

**IF all phases complete AND ready for delivery:**

```
/dt:workflow:07-create-pr ./.workflow/core/workflow-core.json
```

**REQUIRED OUTPUT**: You MUST analyze the workflow state and display the exact commands that are currently available. Replace [task-id] and [next-task-id] with actual values from implementation.json.

**FINAL CRITICAL REQUIREMENT**: You MUST conclude your response by displaying the complete next command with ALL parameters specified. Use this exact format:

```
/0x-<command-name> <complete-parameters>
```

Do NOT use placeholder text like [task-id]. Use ACTUAL values from the workflow files.
This requirement is NON-NEGOTIABLE and essential for workflow continuity.

---

**Command Execution:**

Generate code using:

- Workflow core: ${1:?"workflow-core.json path required"}
- Implementation plan: ${2:?"implementation.json path required"}
- Implementing task: ${3:?"task-id required"}
- Target files: ${4:-"auto-detect from task and discovered ecosystem"}

Use discovery-based execution to generate enterprise-grade, secure, performant, and maintainable code that follows discovered project patterns and ecosystem best practices.
