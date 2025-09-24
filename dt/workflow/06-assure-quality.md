---
allowed-tools: Bash, Read, Write, Edit, Grep, Glob, TodoWrite, mcp__sequential-thinking__sequentialthinking, Task
argument-hint: [workflow-core-json] [testing-json] [optional-fix-mode]
description: Execute comprehensive quality assurance using discovered quality tools
---

# Discovery-Based Enterprise Quality Assurance

## Chain Position: 6/7 (Quality Assurance & Validation)

**Input**: Workflow core + testing files + discovered quality tools
**Output**: Quality-validated codebase + comprehensive quality report + updated modular workflow

## CRITICAL REQUIREMENT

This command uses **ONLY discovered quality commands** from project-context.json. NO quality tools or linting commands are hardcoded. ALL quality assurance follows discovered project standards.

<discovery_validation_blocking>
**STEP 1: BLOCKING - Modular Discovery Prerequisites Check**

1. Load workflow-core.json from $1
2. Load testing.json from $2
3. Load project-context.json from ./.workflow/context/project-context.json
4. Check project_context.discoveredTools.discovery_status
5. IF discovery_status != "complete" THEN:
   - Display error: "❌ Quality tools discovery incomplete. Status: {discovery_status}"
   - Display fix: "Run: /dt:workflow:03-plan-implementation $1 first"
   - EXIT COMMAND IMMEDIATELY
6. Validate discovered quality tools exist in project_context.discoveredTools
7. IF lint commands array is empty THEN:
   - Display error: "❌ No quality tools discovered"
   - Display fix: "Re-run: /dt:workflow:03-plan-implementation to discover quality tools"
   - EXIT COMMAND IMMEDIATELY
8. Validate testing.json has populated test strategy
9. ONLY if all discovery requirements met THEN proceed to quality validation
</discovery_validation_blocking>

## Instructions

**CRITICAL REQUIREMENT - NEXT COMMAND DISPLAY**
You MUST display the complete next task command at the end of execution in the exact format:
`/0x-<command-name> <param1> <param2> <...>`

NEVER provide brief notifications like "You can run /0x-<command> now."
ALWAYS show the complete command with all parameters filled in.
This is NON-NEGOTIABLE and MANDATORY for workflow progression.

<expertise_definition>
You are a senior QA lead specializing in:

- Enterprise quality standards enforcement and validation
- Automated quality gate implementation and monitoring
</expertise_definition>

## **DEVELOPMENT PRINCIPLES - NON-NEGOTIABLE**

<critical_development_principles>
**MANDATORY COMPLIANCE - THESE PRINCIPLES OVERRIDE ALL OTHER CONSIDERATIONS**

### **SLON Principles - STRICTLY ENFORCE**

- **Simplicity**: ALWAYS enforce the simplest quality standards that ensure reliability. Complexity is prohibited unless absolutely justified.
- **Lean**: MINIMAL viable quality processes only. NO bloat, NO unnecessary quality gates, NO speculative standards.
- **One thing**: Each quality check MUST validate exactly one clear criterion. NO multi-purpose mega-validations.
- **No overengineering**: RESIST all unnecessary complexity in quality processes. Question every quality abstraction layer.

### **KISS (Keep It Simple, Stupid) - MANDATORY**

- "As simple as possible, but not simpler than necessary"
- Every piece of quality complexity MUST be justified by genuine, immediate need
- DEFAULT to simple, direct quality approaches over elegant abstractions

### **Occam's Razor - CRITICAL ENFORCEMENT**

- Every new quality tool, process, or standard MUST justify its existence
- PREFER existing quality solutions over new ones
- Challenge every "we need to create a new..." quality decision

### **YAGNI (You Aren't Gonna Need It) - BLOCKING REQUIREMENT**

- NEVER implement quality checks because you *MIGHT* need them
- NO unnecessary quality creep - implement ONLY what is actually needed NOW
- NO speculative future-proofing beyond immediate quality requirements
- Challenge every "but what if..." quality scenario

### **DRY (Don't Repeat Yourself) - MANDATORY CHECK**

- SEARCH existing quality processes for similar validation BEFORE creating new quality checks
- USE existing quality tools and standards instead of creating duplicates
- REUSE before rebuild - always question if similar quality validation already exists

### **ENFORCEMENT INTEGRATION POINTS - NON-NEGOTIABLE**

**BEFORE implementing ANY quality check:**

1. **Existing Quality Check**: "Does similar quality validation already exist in this process?"
2. **Complexity Justification**: "Why won't a simpler quality approach work?"
3. **Immediate Need Validation**: "Is this quality check actually needed NOW, not theoretically?"
4. **Abstraction Challenge**: "Can we ensure quality without adding new abstractions?"

**SPECIFIC PROHIBITIONS:**

- NO "future-proof" quality processes beyond immediate requirements
- NO elegant quality abstractions without clear, immediate benefit
- NO custom quality framework creation when existing solutions exist
- NO speculative quality features or "nice-to-have" validations
- NO complex quality patterns when simple ones suffice

**REQUIRED VALIDATION FOR EVERY QUALITY DECISION:**

- Document why simpler quality approaches won't work
- Prove immediate quality necessity (not theoretical future needs)
- Show existing quality solutions were evaluated and found insufficient
- Justify any new quality abstraction or complexity with concrete benefits

These principles are **MANDATORY** and **NON-NEGOTIABLE**. Any quality assurance process must demonstrate compliance with ALL principles or explicitly justify why deviation is absolutely necessary.
</critical_development_principles>

- Code quality metrics analysis and improvement
- Security vulnerability assessment and remediation
- Performance benchmarking and optimization guidance
- Continuous integration and deployment quality assurance
</expertise_definition>

<systematic_quality_validation>
Execute comprehensive quality validation in systematic order:

**Phase 1: Code Quality Foundation**

- Linting and style validation (zero errors required)
- Type checking and compilation verification
- Code complexity and maintainability analysis
- Documentation completeness validation

**Phase 2: Test Quality Assurance**

- Test execution with 100% pass rate requirement
- Code coverage analysis (85%+ threshold)
- Test quality and effectiveness assessment
- Performance test benchmark validation

**Phase 3: Security and Compliance**

- Static application security testing (SAST)
- Dependency vulnerability scanning
- Security best practices validation
- Compliance requirement verification

**Phase 4: Performance and Reliability**

- Performance benchmark execution
- Load testing and scalability validation
- Error handling and resilience testing
- Resource usage and efficiency analysis

**Phase 5: Enterprise Standards Compliance**

- Code review checklist validation
- Documentation standards compliance
- Deployment readiness assessment
- Quality metrics reporting and analysis

**Phase 6: AI Agent Quality Validation**

- Invoke Security Review Agent for comprehensive vulnerability analysis
- Invoke Performance Review Agent for optimization assessment
- Invoke Architecture Review Agent for design pattern validation
- Invoke Code Quality Review Agent for maintainability analysis
- Invoke E2E Testing Agent for integration validation
- Invoke Application Runner Agent for runtime verification
- Synthesize all AI agent findings into quality assessment
</systematic_quality_validation>

<enterprise_quality_gates_blocking>
**STEP 2: BLOCKING - Modular Quality Gate Execution**

1. Extract and execute first lint command from project context
2. IF exit_code != 0 THEN:
   - Display error: "❌ Linting failed"
   - Display output: {lint_output}
   - Display fix: "Fix linting errors before proceeding"

   - # Write QA failure details for Command 04 to access

   - mkdir -p ./.workflow/execution
   - cat > ./.workflow/execution/qa-results.json <<EOF
{
  "status": "failed",
  "timestamp": "$(date -u +"%Y-%m-%dT%H:%M:%SZ")",
  "failureType": "linting",
  "details": {
    "command": "${lint_cmd}",
    "exitCode": ${exit_code},
    "output": "${lint_output}",
    "actualValue": "linting errors found",
    "expectedValue": "zero linting errors"
  },
  "remediation": "Fix linting errors in the affected files before proceeding",
  "suggestedCommand": "/dt:workflow:04-generate-code ./.workflow/core/workflow-core.json ./.workflow/implementation/implementation.json TASK-1.1"
}
EOF
   - EXIT IMMEDIATELY
3. Extract and execute type check command (if exists) from project context
4. IF exit_code != 0 THEN:
   - Display error: "❌ Type checking failed"
   - Display output: {type_check_output}
   - Display fix: "Fix type errors before proceeding"

   - # Write QA failure details for Command 04 to access

   - mkdir -p ./.workflow/execution
   - cat > ./.workflow/execution/qa-results.json <<EOF
{
  "status": "failed",
  "timestamp": "$(date -u +"%Y-%m-%dT%H:%M:%SZ")",
  "failureType": "typecheck",
  "details": {
    "command": "${type_check_cmd}",
    "exitCode": ${exit_code},
    "output": "${type_check_output}",
    "actualValue": "type errors found",
    "expectedValue": "zero type errors"
  },
  "remediation": "Fix type errors in the affected files before proceeding",
  "suggestedCommand": "/dt:workflow:04-generate-code ./.workflow/core/workflow-core.json ./.workflow/implementation/implementation.json TASK-1.1"
}
EOF
   - EXIT IMMEDIATELY

**STEP 3: BLOCKING - Testing Gate Execution**

1. Extract and execute test commands from discovered tools
2. IF exit_code != 0 THEN:
   - Display error: "❌ Tests failed"
   - Display output: {test_output}
   - Display fix: "Fix failing tests before proceeding"

   - # Write QA failure details for Command 04 to access

   - mkdir -p ./.workflow/execution
   - cat > ./.workflow/execution/qa-results.json <<EOF
{
  "status": "failed",
  "timestamp": "$(date -u +"%Y-%m-%dT%H:%M:%SZ")",
  "failureType": "tests",
  "details": {
    "command": "${test_cmd}",
    "exitCode": ${exit_code},
    "output": "${test_output}",
    "actualValue": "tests failing",
    "expectedValue": "all tests passing"
  },
  "remediation": "Fix failing tests before proceeding",
  "suggestedCommand": "/dt:workflow:04-generate-code ./.workflow/core/workflow-core.json ./.workflow/implementation/implementation.json TASK-1.1"
}
EOF
   - EXIT IMMEDIATELY
3. Extract and execute test coverage commands from discovered tools
4. Parse coverage percentage from output
5. IF coverage < threshold THEN:
   - Display error: "❌ Coverage {actual}% below {threshold}% threshold"
   - Display fix: "Add tests to reach required coverage"

   - # Write QA failure details for Command 04 to access

   - mkdir -p ./.workflow/execution
   - cat > ./.workflow/execution/qa-results.json <<EOF
{
  "status": "failed",
  "timestamp": "$(date -u +"%Y-%m-%dT%H:%M:%SZ")",
  "failureType": "coverage",
  "details": {
    "command": "${coverage_cmd}",
    "actualValue": "${actual_coverage}%",
    "expectedValue": "${threshold}%",
    "uncoveredFiles": [],
    "output": "${coverage_output}"
  },
  "remediation": "Add tests to reach required coverage of ${threshold}%",
  "suggestedCommand": "/dt:workflow:05-architect-tests ./.workflow/core/workflow-core.json ./.workflow/implementation/implementation.json"
}
EOF
   - EXIT IMMEDIATELY

**STEP 4: BLOCKING - Security Gate Execution**

1. Extract and execute security scan commands from discovered tools (if exists)
2. IF high_severity_vulnerabilities > 0 THEN:
   - Display error: "❌ {count} high-severity vulnerabilities found"
   - Display vulnerabilities: {vulnerability_list}
   - Display fix: "Fix high-severity vulnerabilities before proceeding"
   - EXIT IMMEDIATELY
3. Extract and execute dependency audit commands from discovered tools (if exists)
4. IF vulnerable_dependencies > 0 THEN:
   - Display error: "❌ {count} vulnerable dependencies found"
   - Display fix: "Update vulnerable dependencies before proceeding"
   - EXIT IMMEDIATELY

**STEP 5: BLOCKING - Performance Gate Execution**

1. Extract and execute performance benchmark commands from discovered tools (if exists)
2. Parse performance metrics from output
3. IF response_time > acceptable_limits THEN:
   - Display error: "❌ Performance below threshold: {actual}ms > {limit}ms"
   - Display fix: "Optimize performance before proceeding"
   - EXIT IMMEDIATELY
4. IF memory_usage > efficiency_targets THEN:
   - Display error: "❌ Memory usage too high: {actual}MB > {limit}MB"
   - Display fix: "Reduce memory usage before proceeding"
   - EXIT IMMEDIATELY

**ENFORCEMENT RULE**: ALL quality gates must pass. If ANY gate fails, EXIT IMMEDIATELY with specific remediation guidance. No proceeding with failing quality gates.
</enterprise_quality_gates_blocking>

<fix_mode_capability>
When fix-mode is enabled (${2:-"report-only"}):

- Automatically fix linting and formatting issues
- Update dependencies with security vulnerabilities
- Optimize performance bottlenecks where possible
- Enhance documentation and code comments
- Improve test coverage for uncovered areas
</fix_mode_capability>

## Execution Process

<cross_platform_quality_efficiency>
**CROSS-PLATFORM TOKEN EFFICIENCY FOR QUALITY ASSURANCE**

**Universal jq patterns (work on Bash, PowerShell, CMD):**

```bash
# Extract quality gate configuration (< 200 tokens)
jq '.quality_gate_configuration // {}' workflow.json

# Get validation thresholds and limits (< 100 tokens)
jq '.quality_gate_configuration.validation_thresholds // {}' workflow.json

# Extract all test commands for execution (< 50 tokens)
jq -r '.quality_gate_configuration.project_wide_gates.test_commands[]?' workflow.json

# Get performance benchmarks (< 100 tokens)
jq '.quality_gate_configuration.validation_thresholds | {build_time_max: .build_time_max_seconds, memory_max: .memory_usage_max_mb}' workflow.json
```

**Platform-specific examples:**

- **Bash/zsh:** `COVERAGE_MIN=$(jq -r '.quality_gate_configuration.validation_thresholds.test_coverage_minimum // 85' workflow.json)`
- **PowerShell:** `$COVERAGE_MIN = jq -r '.quality_gate_configuration.validation_thresholds.test_coverage_minimum // 85' workflow.json`
- **CMD:** `jq -r ".quality_gate_configuration.validation_thresholds.test_coverage_minimum // 85" workflow.json > coverage.txt`
</cross_platform_quality_efficiency>

### Step 1: Extract Quality Configuration and Setup

```bash
# Extract only necessary data using jq for token efficiency from modular files
WORKFLOW_CORE_FILE="${1:?'workflow-core.json path required'}"
TESTING_FILE="${2:?'testing.json path required'}"
PROJECT_CONTEXT_FILE="./.workflow/context/project-context.json"

# 1. Get quality gate configuration from project context
QUALITY_CONFIG=$(jq '.quality_gates // {}' "$PROJECT_CONTEXT_FILE")

# 2. Get validation thresholds from industry standards
VALIDATION_THRESHOLDS=$(jq '.industry_standards.quality_thresholds // {}' "$PROJECT_CONTEXT_FILE")

# 3. Extract discovered tools for validation commands
PROJECT_GATES=$(jq '.discoveredTools // {}' "$PROJECT_CONTEXT_FILE")

# 4. Get technology stack for tooling detection
TECH_STACK=$(jq '.ecosystem // null' "$PROJECT_CONTEXT_FILE")

# 5. Get task count for progress tracking from implementation
TASK_COUNT=$(jq '.tasks.atomicTasks | length' "./.workflow/implementation/implementation.json" 2>/dev/null || echo "0")

echo "🔍 Quality Assurance Setup: $TASK_COUNT tasks to validate"
echo "📊 Coverage Threshold: $(echo "$VALIDATION_THRESHOLDS" | jq -r '.test_coverage_minimum // 85')%"

Discover project structure and tooling:
- Build system and package manager (from TECH_STACK)
- Test framework and runners (from PROJECT_GATES)
- Linting and formatting tools (from PROJECT_GATES)
- Security scanning capabilities (from PROJECT_GATES)
- Performance testing setup (from VALIDATION_THRESHOLDS)
```

### Step 2: Code Quality Validation

```
Execute systematic code quality checks:

1. Linting and Style Validation:
   - Run configured linters (ESLint, Pylint, etc.)
   - Execute code formatters for consistency
   - Validate naming conventions and standards
   - Check for code smells and anti-patterns

2. Type Safety and Compilation:
   - Run type checkers (TypeScript, MyPy, etc.)
   - Validate compilation without errors
   - Check for type safety violations
   - Verify import and dependency resolution

3. Code Complexity Analysis:
   - Measure cyclomatic complexity
   - Analyze code maintainability metrics
   - Check for excessive nesting and length
   - Validate adherence to SOLID principles
```

### Step 3: Test Quality Assurance

```
Execute comprehensive testing validation:

1. Test Execution and Validation:
   - Run complete test suite (unit, integration, E2E)
   - Validate 100% test pass rate
   - Check test execution performance
   - Analyze test reliability and flakiness

2. Coverage Analysis:
   - Generate code coverage reports
   - Validate 85%+ coverage threshold
   - Identify uncovered critical paths
   - Analyze coverage quality and meaningfulness

3. Test Quality Assessment:
   - Review test effectiveness and assertions
   - Validate test data and scenario coverage
   - Check for test isolation and independence
   - Assess performance test benchmark compliance
```

### Step 4: Security and Compliance Validation

```
Execute security and compliance checks:

1. Static Application Security Testing (SAST):
   - Run security analysis tools
   - Check for common vulnerabilities (OWASP Top 10)
   - Validate input sanitization and validation
   - Review authentication and authorization

2. Dependency Security Scanning:
   - Scan for vulnerable dependencies
   - Check for outdated packages with security issues
   - Validate license compliance
   - Review third-party component security

3. Security Best Practices Validation:
   - Check for hardcoded secrets or credentials
   - Validate secure communication protocols
   - Review data encryption and protection
   - Assess security configuration compliance
```

### Step 5: Performance and Reliability Validation

```
Execute performance and reliability checks:

1. Performance Benchmark Execution:
   - Run performance tests and benchmarks
   - Validate response time requirements
   - Check memory usage and efficiency
   - Assess scalability characteristics

2. Load and Stress Testing:
   - Execute load testing scenarios
   - Validate system behavior under stress
   - Check error handling and recovery
   - Assess resource utilization patterns

3. Reliability and Resilience Testing:
   - Test error handling and recovery mechanisms
   - Validate graceful degradation scenarios
   - Check logging and monitoring effectiveness
   - Assess system stability and consistency
```

### Step 6: Quality Metrics Analysis and Reporting

```
Generate comprehensive quality report:
- Aggregate all quality metrics and results
- Identify areas requiring attention or improvement
- Compare against enterprise quality benchmarks
- Provide actionable recommendations for enhancement
```

## Quality Validation Implementation

**Execute each validation phase systematically:**

1. **Discovery Phase**: Understand project tooling and setup
2. **Code Quality Phase**: Validate linting, typing, and complexity
3. **Testing Phase**: Ensure comprehensive test coverage and execution
4. **Security Phase**: Validate security posture and compliance
5. **Performance Phase**: Benchmark and validate performance characteristics
6. **Reporting Phase**: Generate comprehensive quality assessment

**For each failed quality gate:**

- Provide detailed explanation of the issue
- Suggest specific remediation steps
- If fix-mode enabled, attempt automatic resolution
- Document any manual intervention required

## Fix Mode Operations

**When fix-mode is enabled:**

1. **Automatic Fixes**:
   - Run linting auto-fix capabilities
   - Update insecure dependencies
   - Format code according to standards
   - Add missing documentation templates

2. **Guided Improvements**:
   - Generate missing test cases for uncovered code
   - Enhance error handling in identified areas
   - Optimize identified performance bottlenecks
   - Improve code complexity where possible

3. **Quality Enhancement**:
   - Add comprehensive code comments
   - Improve variable and function naming
   - Refactor overly complex functions
   - Enhance logging and monitoring integration

## Output Process

**Quality Report Generation:**

- Comprehensive quality metrics dashboard
- Detailed analysis of all quality gates
- Specific recommendations for improvement
- Benchmarking against enterprise standards

**Issue Resolution Tracking:**

- List of all identified quality issues
- Prioritization by severity and impact
- Specific remediation steps for each issue
- Automated vs. manual fix requirements

**Workflow JSON Update:**

- Document quality validation results
- Record metrics and benchmark achievements
- Note any quality debt or technical debt
- Update deployment readiness status

```bash
# Token-efficient workflow updates using jq
# Update only quality metrics section instead of rewriting entire JSON
jq --argjson quality_results "$QUALITY_METRICS" \
   --argjson validation_status "$VALIDATION_STATUS" \
   '.quality_metrics = $quality_results |
    .deployment_readiness = $validation_status |
    .last_quality_check = now' \
   "$WORKFLOW_FILE" > updated-workflow.json

# Clear QA results on successful quality assurance completion
if [ "$VALIDATION_STATUS" = "passed" ]; then
    echo "✅ Quality assurance passed - clearing any previous failure context"
    rm -f ./.workflow/execution/qa-results.json
fi
```

## Workflow State Analysis

**MANDATORY**: Analyze current workflow state to determine all available next commands:

1. Load and analyze ./.workflow/implementation/implementation.json for remaining tasks
2. Load and analyze ./.workflow/core/workflow-core.json for phase status
3. Load and analyze ./.workflow/testing/testing.json for test and quality status
4. Analyze quality gate results to determine next actions

**CHAIN OF THOUGHTS ANALYSIS**:

1. Check if quality assurance PASSED or FAILED
2. If FAILED: Determine which areas need fixing (development, testing, or configuration)
3. If PASSED: Check if all workflow phases are complete for PR creation
4. Check for any remaining development or testing tasks
5. Based on analysis, display ALL applicable commands with complete parameters

## Available Next Commands

**MANDATORY**: Display ALL available next commands with complete parameters. Do not use vague language.

**CRITICAL ENFORCEMENT**: You MUST display the complete command format with all parameters filled in. Brief notifications like "You can run /command now" are STRICTLY FORBIDDEN.

**COPY AND EXECUTE**: Choose from these complete commands based on quality assurance results and workflow state:

**IF QUALITY ASSURANCE FAILED - Issues found requiring fixes:**

**For development issues (failing tests, linting errors, security vulnerabilities):**

```
/dt:workflow:04-generate-code ./.workflow/core/workflow-core.json ./.workflow/implementation/implementation.json [fix-task-id]
```

**For test-related issues (coverage, test failures, missing tests):**

```
/dt:workflow:05-architect-tests ./.workflow/core/workflow-core.json ./.workflow/implementation/implementation.json [failing-components] fix-mode
```

**Re-run quality assurance after fixes:**

```
/dt:workflow:06-assure-quality ./.workflow/core/workflow-core.json ./.workflow/testing/testing.json strict
```

**IF QUALITY ASSURANCE PASSED:**

**Check for remaining development tasks:**

```
/dt:workflow:04-generate-code ./.workflow/core/workflow-core.json ./.workflow/implementation/implementation.json [next-task-id]
```

**Create pull request (if all phases complete):**

```
/dt:workflow:07-create-pr ./.workflow/core/workflow-core.json
```

**REQUIRED OUTPUT**: You MUST analyze the quality assurance results and workflow state, then display the exact commands that are currently available. If quality gates failed, show specific fix commands. If quality gates passed, show available next steps. Replace [task-id] values with actual data from workflow files.

**FINAL CRITICAL REQUIREMENT**: You MUST conclude your response by displaying the complete next command with ALL parameters specified. Use this exact format:

```
/dt:workflow:0x-<command-name> <complete-parameters>
```

Do NOT use placeholder text like [task-id]. Use ACTUAL values from the workflow files.
This requirement is NON-NEGOTIABLE and essential for workflow continuity.

---

**Command Execution:**

Validate quality using:

- Workflow core: ${1:?"workflow-core.json path required"}
- Testing data: ${2:?"testing.json path required"}
- Fix mode: ${3:-"report-only"}

Execute comprehensive enterprise quality validation ensuring zero failures, 85%+ coverage, zero linting issues, and full compliance with quality gates.
