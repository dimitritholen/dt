---
allowed-tools: Bash, Read, Write, Grep, mcp__sequential-thinking__sequentialthinking, Task
argument-hint: [workflow-core-json] [optional-pr-template] [optional-branch-name]
description: Create optimized atomic pull request using Chain of Draft methodology
model: sonnet
---

# Enterprise PR Creator with Chain of Draft Optimization

## Chain Position: 7/7 (Pull Request Creation & Delivery)

**Input**: Quality-validated modular workflow files with completed implementation
**Output**: Atomic pull request with comprehensive documentation and metadata

## Instructions

**CRITICAL REQUIREMENT - NEXT COMMAND DISPLAY**
You MUST display the complete next task command at the end of execution in the exact format:
`/0x-<command-name> <param1> <param2> <...>`

NEVER provide brief notifications like "You can run /0x-<command> now."
ALWAYS show the complete command with all parameters filled in.
This is NON-NEGOTIABLE and MANDATORY for workflow progression.

<expertise_definition>
You are a senior DevOps engineer specializing in:

- Atomic commit strategies and Git workflow optimization
- Pull request best practices and code review facilitation
- CI/CD integration and deployment automation
- Documentation and communication excellence
- Enterprise change management and collaboration workflows
</expertise_definition>

<chain_of_draft_methodology>
Use iterative Chain of Draft approach to optimize PR creation:

**Draft 1: Basic PR Structure**

- Analyze changes and create initial commit grouping
- Generate basic PR title and description
- Identify reviewers and stakeholders
- Plan initial metadata and labels

**Draft 2: Content Optimization**

- Enhance PR description with context and rationale
- Improve commit messages for clarity and traceability
- Add comprehensive testing and validation details
- Include deployment and rollback considerations

**Draft 3: Communication Enhancement**

- Optimize for code review efficiency and clarity
- Add visual aids and documentation links
- Include impact analysis and risk assessment
- Enhance stakeholder communication elements

**Draft 4: Final Polish and Validation**

- Validate all quality gates are documented
- Ensure atomic nature and focused scope
- Optimize for merge and deployment success
- Final review of documentation and metadata
</chain_of_draft_methodology>

<atomic_pr_principles>
Ensure PR follows atomic principles:

1. **Single Responsibility**: PR addresses one specific change or feature
2. **Self-Contained**: PR can be understood and reviewed independently
3. **Minimal Scope**: Smallest possible change that delivers value
4. **Quality Complete**: All tests pass, coverage maintained, documentation updated
5. **Reviewable**: Changes are logical, well-documented, and easy to understand
6. **Deployable**: PR can be safely merged and deployed independently
</atomic_pr_principles>

<enterprise_pr_standards>
Apply enterprise PR standards:

**Commit Message Standards:**

- Follow conventional commit format
- Include ticket/issue references
- Provide clear, actionable descriptions
- Maintain consistency with project conventions

**PR Description Standards:**

- Comprehensive summary of changes and rationale
- Clear testing and validation evidence
- Impact analysis and risk assessment
- Deployment and rollback procedures

**Review Process Standards:**

- Appropriate reviewer selection and assignment
- Clear acceptance criteria and checklist
- Documentation of architectural decisions
- Performance and security impact analysis
</enterprise_pr_standards>

<quality_validation_integration>
Before PR creation, validate all enterprise quality gates:

- ✓ All tests passing (100% success rate)
- ✓ Code coverage above 85% threshold
- ✓ Zero linting or style violations
- ✓ Security scans show no high-severity issues
- ✓ Performance benchmarks within acceptable limits
- ✓ Documentation is complete and accurate
</quality_validation_integration>

## Execution Process

<fail_fast_implementation>
STEP 1: MANDATORY - Modular Quality Validation Prerequisites

1. Load workflow-core.json from $1
2. IF file does not exist THEN:
   - Display error: "❌ Workflow core file missing"
   - Display fix: "Run previous workflow commands first"
   - EXIT IMMEDIATELY
3. Load implementation.json from ./.workflow/implementation/implementation.json
4. IF implementation file does not exist or tasks array is empty THEN:
   - Display error: "❌ No completed implementation tasks found"
   - Display fix: "Run: /dt:workflow:04-generate-code to implement features"
   - EXIT IMMEDIATELY
5. Load testing.json from ./.workflow/testing/testing.json
6. IF testing.results.overall_status != "PASSED" THEN:
   - Display error: "❌ Quality validation incomplete or failed"
   - Display fix: "Run: /dt:workflow:06-assure-quality until all gates pass"
   - EXIT IMMEDIATELY
7. ONLY if all prerequisites met THEN proceed to Step 2
</fail_fast_implementation>

## PR Creation Process

<cross_platform_pr_efficiency>
**CROSS-PLATFORM TOKEN EFFICIENCY FOR PR CREATION**

**Universal jq patterns (work on Bash, PowerShell, CMD):**

```bash
# Get completed task summaries from implementation.json (< 200 tokens)
jq '.tasks.atomicTasks[] | select(.status == "completed") | {id, description, type}' ./.workflow/implementation/implementation.json

# Extract quality metrics from testing.json (< 100 tokens)
jq '.results // {}' ./.workflow/testing/testing.json

# Get project metadata from workflow-core.json (< 50 tokens)
jq '{name: .project.name, type: .project.type, description: .project.description}' ./.workflow/core/workflow-core.json

# Extract AI agent review results from testing.json (< 300 tokens)
jq '.agent_reviews // {}' ./.workflow/testing/testing.json
```

**Platform-specific assignment examples:**

- **Bash/zsh:** `COMPLETED_TASKS=$(jq '.tasks.atomicTasks[] | select(.status == "completed")' ./.workflow/implementation/implementation.json)`
- **PowerShell:** `$COMPLETED_TASKS = jq '.tasks.atomicTasks[] | select(.status == "completed")' ./.workflow/implementation/implementation.json`
- **CMD:** `jq ".tasks.atomicTasks[] | select(.status == \"completed\")" ./.workflow/implementation/implementation.json > completed.json`

**Token efficiency:** Extract only PR-relevant data (< 500 tokens) vs entire workflow JSON
</cross_platform_pr_efficiency>

### Step 1: Extract PR Context and Analyze Changes

**Cross-platform approach - use appropriate variable assignment for your shell:**

```bash
# 1. Get project metadata for PR context (< 100 tokens)
jq '{name: .project_name // "unknown", type: .project_type // "unknown", description: .project_description // "", size: .project_size // "medium"}' "$WORKFLOW_FILE"

# 2. Get completed tasks summary (< 200 tokens)
jq '[.tasks[] | select(.status == "completed") | {id, description, type, quality_passed: (.quality_gates.success_criteria.all_tests_pass // false)}]' "$WORKFLOW_FILE"

# 3. Extract quality metrics for PR evidence (< 100 tokens)
jq '.quality_metrics // {}' "$WORKFLOW_FILE"

# 4. Get AI agent review results (< 300 tokens)
jq '.ai_agent_reviews // {}' "$WORKFLOW_FILE"

# 5. Get deployment readiness status (< 50 tokens)
jq '.deployment_readiness // "pending"' "$WORKFLOW_FILE"

echo "📋 Cross-platform PR context extraction complete - <750 tokens total"

# Use platform-appropriate assignment: $() for Bash, direct for PowerShell, temp files for CMD
# Analyze: completed tasks, quality compliance, AI reviews, deployment readiness
```

### Step 2: Git Status and Preparation

```
Execute Git analysis:
- Check current branch status
- Analyze staged and unstaged changes
- Validate commit history and structure
- Ensure clean working directory
```

### Step 3: Chain of Draft PR Optimization

**Draft 1: Initial PR Structure**

- Create atomic commit grouping strategy
- Generate preliminary PR title following conventions
- Draft basic description with change summary
- Plan AI agent review orchestration strategy

**Draft 2: AI Agent Review Orchestration**

- Invoke Security Review Agent for vulnerability analysis
- Invoke Performance Review Agent for optimization assessment
- Invoke Architecture Review Agent for design pattern validation
- Invoke Code Quality Review Agent for maintainability analysis
- Invoke E2E Testing Agent for integration validation
- Synthesize all AI agent findings into comprehensive review

**Draft 3: Content Enhancement with AI Insights**

- Expand PR description with AI agent findings
- Include detailed testing and validation evidence from agents
- Add architectural decisions and trade-offs from architecture review
- Document performance and security considerations from specialized agents

**Draft 4: Communication Optimization**

- Enhance readability and review efficiency
- Add visual elements (code samples, diagrams)
- Include impact analysis and risk assessment from AI agents
- Optimize stakeholder communication with AI-generated insights

**Draft 5: Final Validation and Polish**

- Validate atomic nature and focused scope
- Ensure all AI agent evidence is documented
- Optimize commit messages and metadata
- Final review against enterprise standards with AI validation

### Step 4: Commit Message Generation and Optimization

```
For each logical commit unit:
- Generate conventional commit messages
- Include appropriate scope and type
- Reference related issues and tickets
- Ensure traceability and clarity
```

### Step 5: PR Metadata and Configuration

```
Configure comprehensive PR metadata:
- Appropriate labels for categorization
- Milestone and project associations
- Review assignment and approval requirements
- CI/CD pipeline integration settings
```

### Step 6: Quality Evidence Documentation

```
Document comprehensive quality evidence:
- Test execution results and coverage reports
- Security scan results and compliance validation
- Performance benchmark achievements
- Code review checklist completion
```

## AI Agent Review Orchestration

**Systematic AI-driven code review process:**

### **Phase 1: Parallel Agent Invocation**

Execute all AI agents simultaneously for comprehensive analysis:

```
1. Security Review Agent: Vulnerability and OWASP compliance analysis
2. Performance Review Agent: Optimization and bottleneck identification
3. Architecture Review Agent: Design pattern and SOLID principles validation
4. Code Quality Review Agent: Maintainability and clean code assessment
5. E2E Testing Agent: Integration and workflow validation
```

### **Phase 2: Agent Findings Synthesis**

Consolidate all AI agent reports into comprehensive review:

- **Security Analysis**: Vulnerability findings and remediation guidance
- **Performance Assessment**: Optimization opportunities and metrics
- **Architecture Evaluation**: Design quality and improvement recommendations
- **Code Quality Review**: Maintainability issues and refactoring suggestions
- **Integration Validation**: E2E test results and workflow verification

### **Phase 3: AI Review Documentation**

Generate PR documentation enriched with AI insights:

- Automated quality evidence compilation
- Risk assessment from multiple expert perspectives
- Specific improvement recommendations with priority levels
- Comprehensive validation results from all review dimensions

## Chain of Draft Implementation

**Iteratively refine PR quality through AI-enhanced improvements:**

1. **Initial Draft**: Basic structure with AI agent orchestration plan
2. **AI Review Draft**: Execute parallel agent reviews and collect findings
3. **Content Enhancement Draft**: Integrate AI insights into PR documentation
4. **Communication Draft**: Optimize for stakeholder understanding with AI evidence
5. **Final Draft**: Complete, AI-validated, enterprise-ready PR

**Each draft should improve:**

- Clarity and comprehensiveness of AI-generated documentation
- Evidence of quality and testing thoroughness from specialized agents
- Communication effectiveness enhanced by AI insights
- Compliance with enterprise standards validated by AI experts

## Enterprise PR Template Structure

**PR Title Format:**

```
[type](scope): brief description

Examples:
feat(auth): implement OAuth2 authentication flow
fix(api): resolve race condition in user creation
docs(readme): update deployment instructions
```

**AI-Enhanced PR Description Template:**

```
## Summary
Brief description of changes and business value

## Changes Made
- Detailed list of specific changes
- Technical implementation details
- Architectural decisions and rationale

## AI Agent Review Summary
### 🛡️ Security Review
{SECURITY_AGENT_FINDINGS}

### ⚡ Performance Review
{PERFORMANCE_AGENT_FINDINGS}

### 🏗️ Architecture Review
{ARCHITECTURE_AGENT_FINDINGS}

### 🔍 Code Quality Review
{CODE_QUALITY_AGENT_FINDINGS}

### 🧪 Integration Testing
{E2E_TESTING_AGENT_FINDINGS}

## Testing Evidence
- Test execution results (100% pass rate)
- Coverage reports (85%+ maintained)
- Performance benchmark results from AI analysis
- Security validation outcomes from AI scanning
- Runtime validation from Application Runner Agent

## AI-Validated Quality Assurance
- [ ] All tests passing (validated by E2E Testing Agent)
- [ ] Code coverage maintained above 85% (validated by Code Quality Agent)
- [ ] Linting and style checks passing (validated by Code Quality Agent)
- [ ] Security scans completed with no high-severity issues (validated by Security Agent)
- [ ] Performance requirements met (validated by Performance Agent)
- [ ] Architecture standards maintained (validated by Architecture Agent)
- [ ] Application runs successfully (validated by Application Runner Agent)
- [ ] Documentation updated

## Deployment Considerations
- Deployment strategy and requirements
- Rollback procedures and considerations
- Monitoring and validation plans
- Feature flag or configuration changes

## Review Focus Areas
- Specific areas requiring reviewer attention
- Architectural decisions for validation
- Security and performance considerations
- Integration and compatibility concerns
```

## Output Process

**Git Operations:**

- Create appropriately named feature branch (if needed)
- Generate atomic commits with optimized messages
- Push changes with proper upstream tracking
- Validate remote synchronization

**PR Creation:**

- Generate comprehensive PR using optimized template
- Configure appropriate metadata and labels
- Assign reviewers and set approval requirements
- Integrate with CI/CD pipeline validation

**Documentation Updates:**

- Update workflow JSON with PR information
- Document delivery completion and success metrics
- Record any lessons learned or process improvements
- Archive workflow state for future reference

```bash
# Token-efficient workflow updates using jq
# Update only PR and completion sections instead of rewriting entire JSON
jq --arg pr_url "$PR_URL" \
   --argjson completion_metrics "$COMPLETION_METRICS" \
   --arg completion_date "$(date -u +%Y-%m-%dT%H:%M:%SZ)" \
   '.pull_request = {url: $pr_url, created_at: $completion_date} |
    .completion_metrics = $completion_metrics |
    .status = "completed" |
    .completed_at = $completion_date' \
   "$WORKFLOW_FILE" > final-workflow.json
```

## Workflow Completion Analysis

**MANDATORY**: Analyze workflow completion status and any remaining tasks:

1. Load and analyze ./.workflow/core/workflow-core.json for complete workflow status
2. Load and analyze ./.workflow/implementation/implementation.json for all task completion
3. Load and analyze ./.workflow/testing/testing.json for comprehensive quality validation
4. Verify PR creation success and deployment readiness

**CHAIN OF THOUGHTS ANALYSIS**:

1. Check if ALL development tasks in implementation.json have status = "completed"
2. Check if ALL quality gates in testing.json have status = "PASSED"
3. Check if PR was successfully created and is ready for review
4. Identify any remaining workflow tasks or follow-up actions
5. Based on analysis, display completion status and any remaining commands

## Workflow Status Report

**MANDATORY**: Display comprehensive workflow completion status with any remaining actions.

**CRITICAL ENFORCEMENT**: You MUST display the complete command format with all parameters filled in if any tasks remain. Brief notifications like "You can run /command now" are STRICTLY FORBIDDEN.

**WORKFLOW COMPLETION STATUS:**

**✅ SUCCESSFULLY COMPLETED:**

- PR Created: [PR-URL]
- All Development Tasks: [COMPLETED-COUNT]/[TOTAL-COUNT]
- Quality Gates Status: [PASSED/FAILED]
- Test Coverage: [COVERAGE-PERCENTAGE]%
- Security Validation: [PASSED/FAILED]
- Performance Validation: [PASSED/FAILED]

**REMAINING ACTIONS (if any):**

**IF any development tasks remain incomplete:**

```
/dt:workflow:04-generate-code ./.workflow/core/workflow-core.json ./.workflow/implementation/implementation.json [remaining-task-id]
```

**IF any quality gates failed:**

```
/dt:workflow:06-assure-quality ./.workflow/core/workflow-core.json ./.workflow/testing/testing.json fix-mode
```

**IF all complete - Next Steps:**

- **PR Review**: Share PR with team for code review
- **CI/CD Pipeline**: Monitor automated build and test execution
- **Deployment**: Prepare for deployment after PR approval
- **Monitoring**: Set up post-deployment monitoring and validation

**COMPLETION SUMMARY:**

- Provide PR URL and tracking information
- Summarize quality achievements and compliance
- Document any follow-up actions required
- Celebrate successful enterprise delivery!

**REQUIRED OUTPUT**: You MUST analyze the complete workflow state and display actual completion status with specific metrics. If anything remains incomplete, show the exact commands needed to finish the workflow.

**FINAL CRITICAL REQUIREMENT**: If any workflow tasks remain incomplete, you MUST conclude your response by displaying the complete next command with ALL parameters specified. Use this exact format:

```
/dt:workflow:0x-<command-name> <complete-parameters>
```

Do NOT use placeholder text like [task-id]. Use ACTUAL values from the workflow files.
This requirement is NON-NEGOTIABLE and essential for workflow continuity.

---

**Command Execution:**

Create PR using:

- Workflow core: ${1:?"workflow-core.json path required"}
- PR template: ${2:-"enterprise-standard"}
- Branch name: ${3:-"auto-generate"}

Use Chain of Draft methodology to create enterprise-grade atomic pull request with comprehensive documentation, quality evidence, and optimized reviewer experience.
