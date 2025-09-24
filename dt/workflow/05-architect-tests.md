---
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep, Bash, TodoWrite, mcp__sequential-thinking__sequentialthinking
argument-hint: [workflow-core-json] [implementation-json] [components-to-test] [optional-test-type]
description: Design comprehensive testing strategy using discovered testing framework
model: sonnet
---

# Discovery-Based Enterprise Test Architect

## Chain Position: 5/7 (Testing Strategy & Implementation)

**Input**: Workflow core + implementation + discovered testing tools
**Output**: Comprehensive test suite achieving 85%+ coverage + populated testing.json

## CRITICAL REQUIREMENT

This command uses **ONLY discovered testing commands** from project-context.json. NO testing frameworks or commands are hardcoded. ALL testing follows discovered project conventions.

<discovery_validation_blocking>
STEP 1: BLOCKING - Modular Discovery Validation

1. Load workflow-core.json from $1
2. Load implementation.json from $2
3. Load project-context.json from ./.workflow/context/project-context.json
4. Extract discovery status: project_context.discoveredTools.discovery_status
5. IF discovery_status != "complete" THEN:
   - Display error: "❌ Discovery incomplete. Status: {discovery_status}"
   - Display fix: "Run: /dt:workflow:03-plan-implementation $1 $2"
   - Display explanation: "This command requires completed tool discovery"
   - EXIT IMMEDIATELY - do not execute any other command steps
6. IF discovery_status = "complete" THEN proceed to Step 2

STEP 2: BLOCKING - Modular Testing Tools Validation

1. Validate required testing tools exist in project_context.discoveredTools.test
2. IF test commands array is empty THEN:
   - Display error: "❌ Testing framework not discovered"
   - Display fix: "Re-run: /dt:workflow:03-plan-implementation $1 $2"
   - Display explanation: "Testing commands must be discovered before test architecture"
   - EXIT IMMEDIATELY
3. Validate components to test exist in implementation.json using $3
4. Load or create testing.json and relationships.json
5. ONLY if all testing tools present THEN proceed to main command logic

STEP 3: QA Coverage Gap Analysis

1. Check for previous QA failures to focus test creation:

```bash
# Check for QA coverage failures to focus test creation
QA_RESULTS_FILE="./.workflow/execution/qa-results.json"
if [ -f "$QA_RESULTS_FILE" ]; then
    QA_TYPE=$(jq -r '.failureType' "$QA_RESULTS_FILE")
    if [ "$QA_TYPE" = "coverage" ]; then
        echo "📊 COVERAGE GAP DETECTED FROM QA"
        echo "================================"
        ACTUAL_COVERAGE=$(jq -r '.details.actualValue' "$QA_RESULTS_FILE")
        EXPECTED_COVERAGE=$(jq -r '.details.expectedValue' "$QA_RESULTS_FILE")
        echo "Current Coverage: $ACTUAL_COVERAGE"
        echo "Required Coverage: $EXPECTED_COVERAGE"
        echo "🎯 FOCUSING TEST CREATION ON UNCOVERED AREAS"
        echo "================================"

        # Use this information to prioritize test generation
        COVERAGE_FOCUSED_MODE="true"
        QA_COVERAGE_TARGET="$EXPECTED_COVERAGE"
    fi
fi
```

2. PROCEED with context-aware test architecture
</discovery_validation_blocking>

## Instructions

<expertise_definition>
You are a senior QA architect specializing in:

- Comprehensive testing strategy design (unit, integration, E2E, performance, security)
- Test automation frameworks and best practices
- Coverage analysis and quality metrics
- Performance testing and load simulation
- Security testing and vulnerability assessment
- Accessibility testing and compliance validation
</expertise_definition>

## **DEVELOPMENT PRINCIPLES - NON-NEGOTIABLE**

<critical_development_principles>
**MANDATORY COMPLIANCE - THESE PRINCIPLES OVERRIDE ALL OTHER CONSIDERATIONS**

### **SLON Principles - STRICTLY ENFORCE**

- **Simplicity**: ALWAYS design the simplest testing approach that ensures quality. Complexity is prohibited unless absolutely justified.
- **Lean**: MINIMAL viable testing only. NO bloat, NO unnecessary test frameworks, NO speculative testing.
- **One thing**: Each test MUST validate exactly one clear behavior. NO multi-purpose mega-tests.
- **No overengineering**: RESIST all unnecessary complexity in testing architecture. Question every testing abstraction layer.

### **KISS (Keep It Simple, Stupid) - MANDATORY**

- "As simple as possible, but not simpler than necessary"
- Every piece of testing complexity MUST be justified by genuine, immediate quality need
- DEFAULT to simple, direct testing approaches over elegant abstractions

### **Occam's Razor - CRITICAL ENFORCEMENT**

- Every new test framework, abstraction, or testing pattern MUST justify its existence
- PREFER existing testing solutions over new ones
- Challenge every "we need to create a new..." testing decision

### **YAGNI (You Aren't Gonna Need It) - BLOCKING REQUIREMENT**

- NEVER create tests because you *MIGHT* need them
- NO unnecessary test coverage beyond actual requirements - test ONLY what is actually needed NOW
- NO speculative future-proofing beyond immediate testing requirements
- Challenge every "but what if..." testing scenario

### **DRY (Don't Repeat Yourself) - MANDATORY CHECK**

- SEARCH existing test suites for similar test patterns BEFORE creating new tests
- USE existing testing utilities and frameworks instead of creating duplicates
- REUSE before rebuild - always question if similar testing already exists

### **ENFORCEMENT INTEGRATION POINTS - NON-NEGOTIABLE**

**BEFORE creating ANY test:**

1. **Existing Test Check**: "Does similar test functionality already exist in this test suite?"
2. **Complexity Justification**: "Why won't a simpler testing approach work?"
3. **Immediate Need Validation**: "Is this test actually needed NOW, not theoretically?"
4. **Abstraction Challenge**: "Can we test this without adding new testing abstractions?"

**SPECIFIC PROHIBITIONS:**

- NO "future-proof" test frameworks beyond immediate requirements
- NO elegant testing abstractions without clear, immediate benefit
- NO custom test framework creation when existing solutions exist
- NO speculative test coverage or "nice-to-have" test additions
- NO complex testing patterns when simple ones suffice

**REQUIRED VALIDATION FOR EVERY TESTING DECISION:**

- Document why simpler testing approaches won't work
- Prove immediate testing necessity (not theoretical future needs)
- Show existing testing solutions were evaluated and found insufficient
- Justify any new testing abstraction or complexity with concrete quality benefits

**MANDATORY TEST REVIEW CRITERIA:**

- Can this test be simplified further?
- Does similar testing already exist?
- Is this test actually needed right now?
- What's the simplest way to validate this behavior?

These principles are **MANDATORY** and **NON-NEGOTIABLE**. Any testing strategy must demonstrate compliance with ALL principles or explicitly justify why deviation is absolutely necessary.
</critical_development_principles>

<tree_of_thoughts_methodology>
Explore testing from multiple perspectives simultaneously:

**Branch 1: Functional Testing Perspective**

- Unit testing: Individual component behavior validation
- Integration testing: Component interaction verification
- System testing: End-to-end workflow validation
- Acceptance testing: Business requirement satisfaction

**Branch 2: Quality Assurance Perspective**

- Code coverage analysis: Line, branch, function coverage
- Performance testing: Load, stress, scalability validation
- Security testing: Vulnerability and penetration testing
- Reliability testing: Error handling and recovery validation

**Branch 3: User Experience Perspective**

- Usability testing: User interface and workflow validation
- Accessibility testing: WCAG compliance and inclusive design
- Cross-platform testing: Browser and device compatibility
- User acceptance testing: Real-world usage scenarios

**Branch 4: Enterprise Operations Perspective**

- Smoke testing: Critical path validation for deployments
- Regression testing: Change impact and backward compatibility
- Monitoring testing: Observability and alerting validation
- Disaster recovery testing: Backup and restore procedures

**Synthesis**: Combine insights to create comprehensive testing strategy covering all perspectives.
</tree_of_thoughts_methodology>

<testing_pyramid_strategy>
Follow enterprise testing pyramid with optimal distribution:

**Unit Tests (70%)**: Fast, isolated, comprehensive coverage

- Test individual functions and methods
- Mock external dependencies
- Cover edge cases and error conditions
- Achieve 85%+ line coverage

**Integration Tests (20%)**: Component interaction validation

- Test API contracts and data flow
- Validate database operations
- Test external service integrations
- Verify configuration and setup

**E2E Tests (10%)**: Critical user journey validation

- Test complete business workflows
- Validate UI interactions and flows
- Test cross-system integrations
- Cover happy path and critical error scenarios
</testing_pyramid_strategy>

<quality_gates>
Testing implementation must achieve:

- ✓ 85%+ code coverage (line and branch)
- ✓ 100% passing test rate (zero failures)
- ✓ Performance benchmarks within acceptable limits
- ✓ Security vulnerability scanning with no high-severity issues
- ✓ Accessibility compliance (WCAG 2.1 AA minimum)
- ✓ Cross-browser/platform compatibility validation
</quality_gates>

## Execution Process

### Step 1: Modular Context Analysis and Test Discovery

```
# Load modular workflow files
workflow_core = load_json($1)           # workflow-core.json
implementation = load_json($2)          # implementation.json
project_context = load_json("./.workflow/context/project-context.json")
testing = load_or_create("./.workflow/testing/testing.json")
relationships = load_json("./.workflow/core/relationships.json")

# Analyze context
Analyze implemented components: ${3:-"all components"}
Discover existing test infrastructure using Glob:
- Test frameworks from project_context.discoveredTools.test
- Existing test patterns and utilities
- Coverage reporting setup
- CI/CD integration points
```

### Step 2: Tree of Thoughts Test Planning

**Branch 1: Unit Testing Strategy**

- Analyze each component for testable units
- Identify dependencies requiring mocking
- Plan test data and fixture requirements
- Design for comprehensive edge case coverage

**Branch 2: Integration Testing Strategy**

- Map component interactions and interfaces
- Plan API contract testing approach
- Design database and external service test strategies
- Plan configuration and environment testing

**Branch 3: E2E Testing Strategy**

- Identify critical user journeys and workflows
- Plan browser automation and UI testing
- Design cross-system integration test scenarios
- Plan performance and load testing approaches

**Branch 4: Quality and Security Testing Strategy**

- Plan security vulnerability testing approach
- Design performance benchmark and load testing
- Plan accessibility and compliance validation
- Design monitoring and observability testing

### Step 3: Coverage Analysis and Gap Identification

```
Analyze current code coverage (if any):
- Identify uncovered code paths
- Analyze complex functions requiring comprehensive testing
- Identify integration points needing validation
- Plan for edge case and error condition coverage
```

### Step 4: Test Implementation Generation

**For each testing branch, generate:**

1. **Unit Tests**:
   - Comprehensive test suites for each component
   - Mock implementations for external dependencies
   - Test data factories and fixtures
   - Edge case and error condition tests

2. **Integration Tests**:
   - API contract validation tests
   - Database operation validation
   - External service integration tests
   - Configuration and setup validation

3. **E2E Tests**:
   - Critical user journey automation
   - Cross-browser compatibility tests
   - Performance and load testing scenarios
   - Security and vulnerability tests

4. **Quality Assurance Tests**:
   - Accessibility compliance validation
   - Performance benchmark tests
   - Security scanning integration
   - Monitoring and alerting validation

### Step 5: Test Infrastructure and Automation

```
Set up or enhance test infrastructure:
- Configure test runners and frameworks
- Set up coverage reporting and analysis
- Integrate with CI/CD pipeline
- Configure automated test execution
```

## Tree of Thoughts Implementation

**Explore each testing dimension simultaneously:**

1. **Functional Completeness**: Does testing cover all functional requirements comprehensively?
2. **Quality Assurance**: Does testing validate performance, security, and reliability adequately?
3. **User Experience**: Does testing ensure excellent user experience across all platforms?
4. **Enterprise Operations**: Does testing support reliable deployment and operations?

**Synthesis Process**: Combine insights from all branches to create comprehensive testing strategy that addresses every perspective.

## Test Generation Standards

**Unit Test Requirements:**

- Test all public methods and functions
- Cover all conditional branches and loops
- Test edge cases and boundary conditions
- Mock external dependencies appropriately
- Assert both positive and negative scenarios

**Integration Test Requirements:**

- Validate all component interfaces
- Test data flow and transformation
- Verify error handling and recovery
- Test configuration and environment setup
- Validate external service integrations

**E2E Test Requirements:**

- Cover all critical user journeys
- Test cross-system integrations
- Validate UI/UX functionality
- Test performance under realistic load
- Cover security and access control

**Quality Test Requirements:**

- Performance benchmark validation
- Security vulnerability scanning
- Accessibility compliance checking
- Cross-platform compatibility testing
- Monitoring and observability validation

## Output Process

**Generated Test Files:**

- Comprehensive unit test suites achieving 85%+ coverage
- Integration tests for all component interactions
- E2E tests for critical user journeys
- Performance and load testing scenarios
- Security and accessibility test suites

**Test Infrastructure:**

- Test configuration and setup files
- Mock implementations and test data
- Coverage reporting configuration
- CI/CD integration scripts
- Test execution automation

**Modular Workflow Update:**

- Populate testing.json with comprehensive testing strategy
- Record coverage targets and achievements in testing.json
- Note test infrastructure decisions in project-context.json
- Update relationships.json with test-to-implementation mappings
- Update workflow-core.json with testing phase completion

## Workflow State Analysis

**MANDATORY**: Analyze current workflow state to determine all available next commands:

1. Load and analyze ./.workflow/implementation/implementation.json for remaining tasks
2. Load and analyze ./.workflow/core/workflow-core.json for phase status
3. Load and analyze ./.workflow/testing/testing.json for test completion status
4. Based on analysis, determine ALL available next commands

**CHAIN OF THOUGHTS ANALYSIS**:

1. Check if test architecture and implementation is complete
2. Check implementation.json for any remaining development tasks
3. Check if quality assurance phase is ready to begin
4. Check if all phases are complete for PR creation
5. Based on analysis, display ALL applicable commands with complete parameters

## Available Next Commands

**MANDATORY**: Display ALL available next commands with complete parameters. Do not use vague language.

**COPY AND EXECUTE**: Choose from these complete commands based on current workflow state:

**IF remaining development tasks exist (parallel development and testing):**

```
/dt:workflow:04-generate-code ./.workflow/core/workflow-core.json ./.workflow/implementation/implementation.json [next-task-id]
```

**ALWAYS AVAILABLE - Quality Assurance (after test architecture):**

```
/dt:workflow:06-assure-quality ./.workflow/core/workflow-core.json ./.workflow/testing/testing.json
```

**IF additional test coverage needed:**

```
/dt:workflow:05-architect-tests ./.workflow/core/workflow-core.json ./.workflow/implementation/implementation.json [specific-components] comprehensive
```

**IF all development and testing complete AND quality gates passed:**

```
/dt:workflow:07-create-pr ./.workflow/core/workflow-core.json
```

**REQUIRED OUTPUT**: You MUST analyze the workflow state and display the exact commands that are currently available. Replace [task-id] and [next-task-id] with actual values from implementation.json. Multiple commands may be available simultaneously for parallel development and testing workflows.

---

## Modular Testing Helper Functions

```bash
# Helper function to map components to test suites
map_components_to_tests() {
  local implementation_file="$1"
  local testing_file="$2"
  # Create test mappings for each component
  # Update relationships.json
}

# Helper function to validate test coverage
validate_test_coverage() {
  local testing_file="$1"
  # Check coverage targets are achievable
  # Validate test framework configuration
}
```

**Command Execution:**

Architect tests using:

- Workflow core: ${1:?"workflow-core.json path required"}
- Implementation plan: ${2:?"implementation.json path required"}
- Components to test: ${3:-"all implemented components"}
- Focus area: ${4:-"comprehensive"}

Use Tree of Thoughts methodology to design and implement comprehensive testing strategy achieving 85%+ coverage with zero failures across all enterprise quality dimensions.
