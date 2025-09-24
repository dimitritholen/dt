---
allowed-tools: Task, Read, Write, Bash
argument-hint: [prd-file-or-text] [optional-workflow-mode]
description: Execute complete enterprise development workflow from PRD to PR
---

# Complete Enterprise Development Workflow

## Master Command: Full Chain Execution

**Purpose**: Execute the complete enterprise development workflow from PRD analysis to pull request creation using all 7 specialized commands in sequence.

**Input**: PRD document (file path or text content)
**Output**: Production-ready feature with comprehensive documentation, tests, and quality validation

## Workflow Modes

**Mode Options** (${2:-"comprehensive"}):

- `comprehensive`: Full workflow with all quality gates and documentation
- `rapid`: Streamlined workflow for faster development (reduced documentation)
- `parallel`: Optimized for team development with parallel task execution
- `quality-first`: Extra emphasis on testing and quality assurance

## Instructions

<workflow_orchestration>
You are the enterprise development workflow orchestrator. Your role is to coordinate the execution of all 7 specialized commands in the proper sequence, ensuring seamless data flow and maintaining enterprise quality standards throughout the process.

Execute the complete workflow using the Task tool to invoke each specialized command in sequence, monitoring progress and quality at each stage.
</workflow_orchestration>

<enterprise_workflow_execution>
Execute the following workflow sequence:

**Phase 1: Requirements and Architecture (Foundation)**

1. `/dt:workflow:01-analyze-prd` - Analyze PRD with Tree of Thoughts reasoning
2. `/dt:workflow:02-design-architecture` - Design enterprise architecture with Chain of Thoughts

**Phase 2: Implementation Planning and Development**
3. `/dt:workflow:03-plan-implementation` - Plan atomic implementation with Chain of Draft
4. `/dt:workflow:04-generate-code` - Generate enterprise-grade code (iterative for each task)

**Phase 3: Quality Assurance and Delivery**
5. `/dt:workflow:05-architect-tests` - Design comprehensive testing with Tree of Thoughts
6. `/dt:workflow:06-assure-quality` - Execute quality validation with enterprise standards
7. `/dt:workflow:07-create-pr` - Create optimized PR with Chain of Draft

Monitor workflow state and quality gates between each phase.
</enterprise_workflow_execution>

## Execution Process

### Step 1: Workflow Initialization

```
Initialize enterprise workflow with:
- PRD analysis and requirements extraction
- Quality gate configuration based on mode
- Workflow state tracking and monitoring
- Team coordination and parallel task planning
```

### Step 2: Foundation Phase Execution

```
Execute foundation commands in sequence:

1. Analyze PRD:
   - Use Task tool to invoke 01-analyze-prd command
   - Validate comprehensive requirements extraction
   - Ensure business and technical requirements are captured
   - Verify quality gates are properly configured

2. Design Architecture:
   - Use Task tool to invoke 02-design-architecture command
   - Validate enterprise architecture patterns
   - Ensure scalability and security considerations
   - Verify technology stack selections are appropriate
```

### Step 3: Implementation Phase Execution

```
Execute implementation commands:

3. Plan Implementation:
   - Use Task tool to invoke 03-plan-implementation command
   - Validate atomic task breakdown
   - Ensure parallel development opportunities identified
   - Verify quality integration at each phase

4. Generate Code (Iterative):
   - Identify all tasks from implementation plan
   - For each task, use Task tool to invoke 04-generate-code command
   - Monitor code quality and integration at each step
   - Ensure enterprise standards are maintained
   - Validate each task completion before proceeding
```

### Step 4: Quality and Delivery Phase Execution

```
Execute quality and delivery commands:

5. Architect Tests:
   - Use Task tool to invoke 05-architect-tests command
   - Validate comprehensive test coverage (85%+)
   - Ensure all test types are implemented
   - Verify performance and security testing inclusion

6. Assure Quality:
   - Use Task tool to invoke 06-assure-quality command with fix-mode
   - Validate all quality gates pass (100% success required)
   - Ensure zero linting errors and failing tests
   - Verify security scans show no high-severity issues

7. Create PR:
   - Use Task tool to invoke 07-create-pr command
   - Validate atomic PR structure and documentation
   - Ensure comprehensive change documentation
   - Verify deployment readiness and rollback plans
```

### Step 5: Workflow Completion and Validation

```
Complete workflow execution:
- Validate entire workflow completion
- Generate comprehensive delivery report
- Document quality achievements and metrics
- Provide next steps and follow-up actions
```

## Quality Gate Monitoring

**Between Each Phase:**

- Validate JSON schema compliance and data integrity
- Ensure quality standards are maintained or improved
- Verify no regression in previously completed work
- Confirm readiness for next phase execution

**Critical Quality Gates:**

- ✓ Requirements completeness and traceability (Phase 1)
- ✓ Architecture compliance with enterprise standards (Phase 1)
- ✓ Implementation plan supports atomic development (Phase 2)
- ✓ Code quality meets enterprise standards (Phase 2)
- ✓ Test coverage above 85% with 100% pass rate (Phase 3)
- ✓ All quality checks pass without errors (Phase 3)
- ✓ PR is atomic, documented, and deployment-ready (Phase 3)

## Workflow Mode Customization

### Comprehensive Mode (Default)

- Full documentation and quality validation
- Extensive testing and security scanning
- Complete architectural decision documentation
- Comprehensive PR documentation and review process

### Rapid Mode

- Streamlined documentation requirements
- Essential testing with 85% coverage minimum
- Core security validation only
- Simplified PR creation with essential information

### Parallel Mode

- Optimized task breakdown for team development
- Concurrent execution where possible
- Enhanced coordination and integration planning
- Team-specific documentation and handoff procedures

### Quality-First Mode

- Enhanced testing requirements (90%+ coverage)
- Additional security scanning and validation
- Performance benchmarking and optimization
- Extended code review and documentation requirements

## Error Handling and Recovery

**If Any Command Fails:**

1. Analyze failure reason and impact
2. Attempt automatic recovery where possible
3. Provide specific guidance for manual intervention
4. Option to continue workflow from failure point
5. Maintain workflow state for resumption

**Quality Gate Failures:**

1. Identify specific quality violations
2. Provide detailed remediation guidance
3. Option to auto-fix where appropriate
4. Re-execute quality validation after fixes
5. Ensure no compromise in enterprise standards

## Output and Reporting

**Workflow Completion Report:**

- Comprehensive summary of all phases executed
- Quality metrics and achievements documented
- Security validation and compliance status
- Performance benchmarks and optimization notes
- Deployment readiness assessment and next steps

**Deliverables:**

- Production-ready code with comprehensive documentation
- Complete test suite with 85%+ coverage and 100% pass rate
- Quality-validated codebase with zero violations
- Enterprise-grade pull request ready for review and merge
- Comprehensive workflow documentation and audit trail

---

**Command Execution:**

Execute enterprise workflow for: ${1:?"PRD file path or text content required"}
Workflow mode: ${2:-"comprehensive"}

Orchestrate complete enterprise development workflow ensuring quality, security, and compliance at every stage.
