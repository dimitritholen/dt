---
allowed-tools: Read, Bash, mcp__sequential-thinking__sequentialthinking
argument-hint: "[optional-detailed-mode]"
description: "Comprehensive enterprise workflow progress analysis and next action determination"
---

# Enterprise Workflow Progress Check

**Chain Position**: Utility Command (not part of main 1-7 workflow chain)
**Purpose**: Analyze current workflow state by reading modular workflow files and provide comprehensive progress report with next actions.

## Development Principles

- **SLON** (Simple, Logical, Organized, Natural): Clear progress analysis with logical flow
- **KISS** (Keep It Simple, Stupid): Direct state assessment without over-engineering
- **Occam's Razor**: Simplest explanation for current workflow state
- **YAGNI** (You Aren't Gonna Need It): Focus on current state, not speculative features
- **DRY** (Don't Repeat Yourself): Reuse established workflow file patterns

## Input

- **Argument**: `[optional-detailed-mode]` - if "detailed" is passed, show granular task breakdown
- **Requirements**: None (reads existing workflow state)
- **Context**: Analyzes modular workflow files in `.workflow/` directory structure

## Output

- **Primary**: Comprehensive visual progress report with phase completion status
- **Secondary**: Quality metrics, blocking issues identification, next action recommendation
- **Format**: Enterprise-grade progress display with percentages and task counts

## Fail-Fast Validation

### Blocking Requirements

1. **Directory Structure**: Must be run from project root with potential `.workflow/` directory
2. **File Access**: Must have read permissions to workflow files
3. **JSON Integrity**: Workflow files must be valid JSON (graceful degradation if corrupted)

### Non-Blocking Scenarios

- Missing `.workflow/` directory (indicates workflow not started)
- Missing individual workflow files (indicates partial completion)
- Corrupted JSON files (report as validation issues)

## Implementation

```bash
#!/bin/bash

# Enterprise Workflow Progress Check Implementation
# Analyzes current workflow state and provides comprehensive progress report

set -euo pipefail

DETAILED_MODE="${1:-}"
WORKFLOW_DIR=".workflow"

# Color codes for visual formatting
GREEN="\033[32m"
YELLOW="\033[33m"
RED="\033[31m"
BLUE="\033[34m"
RESET="\033[0m"
BOLD="\033[1m"

# Unicode symbols for progress display
CHECK="✅"
PROGRESS="🔄"
PENDING="⏳"
ERROR="❌"
WARNING="⚠️"

echo "🔍 ANALYZING ENTERPRISE WORKFLOW STATE..."
echo ""

# Check if workflow directory exists
if [[ ! -d "$WORKFLOW_DIR" ]]; then
    echo "${YELLOW}${WARNING} No workflow directory found. Workflow not yet started.${RESET}"
    echo ""
    echo "${BOLD}🎯 NEXT RECOMMENDED ACTION:${RESET}"
    echo "Please specify the PRD file to analyze:"
    echo "${BLUE}/dt:workflow:01-analyze-prd [path/to/prd-file]${RESET}"
    echo ""
    echo "Example: /dt:workflow:01-analyze-prd requirements/prd.md"
    exit 0
fi

echo "📂 Workflow directory found. Reading modular workflow files..."
echo ""
```

## Chain of Thought Analysis

Use `mcp__sequential-thinking__sequentialthinking` to comprehensively analyze workflow state:

### Analysis Steps

1. **File Discovery**: Identify which modular workflow files exist
2. **State Parsing**: Extract current phase, completion status, and task progress
3. **Progress Calculation**: Determine completion percentages for each phase
4. **Blocker Identification**: Find any validation failures or incomplete dependencies
5. **Next Action Determination**: Apply decision logic to recommend specific next command
6. **Report Generation**: Format comprehensive progress display

### Decision Logic for Next Command

```
IF .workflow doesn't exist:
→ /dt:workflow:01-analyze-prd [prd-file]

ELSE IF workflow-core.json missing or current_phase is null:
→ /dt:workflow:01-analyze-prd [prd-file]

ELSE IF current_phase == "requirements_analysis" and discovery_status != "complete":
→ /dt:workflow:02-architect-system [workflow-core] [requirements]

ELSE IF current_phase == "architecture_design" and architecture_status != "complete":
→ /dt:workflow:03-plan-implementation [workflow-core] [architecture]

ELSE IF current_phase == "implementation_planning" and planning_status != "complete":
→ /dt:workflow:03-plan-implementation [workflow-core] [architecture]

ELSE IF current_phase == "code_generation" and incomplete tasks exist:
→ /dt:workflow:04-generate-code [workflow-core] [implementation] [next-incomplete-task-id]

ELSE IF validation failures exist:
→ /04.5-validate-task-completion [workflow-core] [implementation] [failed-task-id] strict

ELSE IF current_phase == "code_generation" and all tasks complete but no testing.json:
→ /dt:workflow:05-architect-tests [workflow-core] [implementation]

ELSE IF current_phase == "testing" and testing incomplete:
→ /dt:workflow:05-architect-tests [workflow-core] [implementation]

ELSE IF current_phase == "quality_assurance" and quality not assured:
→ /dt:workflow:06-assure-quality [workflow-core] [testing]

ELSE IF all phases complete:
→ /dt:workflow:07-create-pr [workflow-core]
```

## Workflow File Analysis

### Core State Files

```bash
# Read core workflow state
if [[ -f "$WORKFLOW_DIR/core/workflow-core.json" ]]; then
    echo "📋 Reading core workflow state..."
    # Extract current_phase, project_name, overall_progress
else
    echo "${WARNING} Core workflow file missing - workflow not properly initialized"
fi

# Read project context
if [[ -f "$WORKFLOW_DIR/context/project-context.json" ]]; then
    echo "🔍 Reading project context..."
    # Extract project info, discovered tools, ecosystem
fi

# Read requirements analysis
if [[ -f "$WORKFLOW_DIR/requirements/requirements.json" ]]; then
    echo "📝 Reading requirements analysis..."
    # Extract requirements count, coverage status
fi

# Read architecture design
if [[ -f "$WORKFLOW_DIR/architecture/architecture.json" ]]; then
    echo "🏗️ Reading architecture design..."
    # Extract component count, design status
fi

# Read implementation plan
if [[ -f "$WORKFLOW_DIR/implementation/implementation.json" ]]; then
    echo "⚙️ Reading implementation plan..."
    # Extract task progress, completion status
fi

# Read testing architecture
if [[ -f "$WORKFLOW_DIR/testing/testing.json" ]]; then
    echo "🧪 Reading testing architecture..."
    # Extract test coverage, testing status
fi

# Check execution results
if [[ -d "$WORKFLOW_DIR/execution" ]]; then
    echo "✅ Reading execution results..."
    # Check for validation failures, completion status
fi
```

## Progress Report Format

### Visual Progress Display

```bash
echo "🔄 ENTERPRISE WORKFLOW PROGRESS REPORT"
echo "━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"
echo "📋 Project: $PROJECT_NAME | Current Phase: $CURRENT_PHASE | Overall: $OVERALL_PROGRESS% Complete"
echo "━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"
echo ""
echo "📊 WORKFLOW PHASES:"
echo "$PHASE_1_STATUS 1. Analyze PRD          │ $PHASE_1_COMPLETION  │ $PHASE_1_DETAILS"
echo "$PHASE_2_STATUS 2. Design Architecture  │ $PHASE_2_COMPLETION  │ $PHASE_2_DETAILS"
echo "$PHASE_3_STATUS 3. Plan Implementation  │ $PHASE_3_COMPLETION  │ $PHASE_3_DETAILS"
echo "$PHASE_4_STATUS 4. Generate Code        │ $PHASE_4_COMPLETION  │ $PHASE_4_DETAILS"
echo "$PHASE_5_STATUS 5. Architect Tests      │ $PHASE_5_COMPLETION  │ $PHASE_5_DETAILS"
echo "$PHASE_6_STATUS 6. Assure Quality      │ $PHASE_6_COMPLETION  │ $PHASE_6_DETAILS"
echo "$PHASE_7_STATUS 7. Create PR           │ $PHASE_7_COMPLETION  │ $PHASE_7_DETAILS"
echo ""
echo "🔍 CURRENT PHASE DETAILS:"
echo "Phase: $CURRENT_PHASE_NAME"
echo "Status: $CURRENT_PHASE_STATUS"
echo "Progress: $CURRENT_PHASE_PROGRESS% ($COMPLETED_TASKS/$TOTAL_TASKS tasks)"
echo ""
echo "📈 QUALITY METRICS:"
echo "• Requirements Coverage: $REQ_COVERAGE%"
echo "• Architecture Completeness: $ARCH_COMPLETENESS%"
echo "• Implementation Progress: $IMPL_PROGRESS%"
echo "• Test Coverage: $TEST_COVERAGE%"
echo "• Quality Score: $QUALITY_SCORE%"
echo ""

if [[ "$DETAILED_MODE" == "detailed" ]]; then
    echo "📋 DETAILED TASK BREAKDOWN:"
    # Show granular task status
    echo ""
fi

if [[ -n "$BLOCKING_ISSUES" ]]; then
    echo "🚨 BLOCKING ISSUES:"
    echo "$BLOCKING_ISSUES"
    echo ""
fi
```

## Next Command Determination

Implement the decision logic using Chain of Thought analysis to provide the exact next command with actual parameters:

```bash
echo "${BOLD}🎯 NEXT RECOMMENDED ACTION:${RESET}"
echo "$NEXT_COMMAND"
echo ""
echo "$NEXT_COMMAND_EXPLANATION"
```

### Complete Command Examples

- `/dt:workflow:01-analyze-prd requirements/prd.md`
- `/dt:workflow:02-architect-system .workflow/core/workflow-core.json .workflow/requirements/requirements.json`
- `/dt:workflow:03-plan-implementation .workflow/core/workflow-core.json .workflow/architecture/architecture.json`
- `/dt:workflow:04-generate-code .workflow/core/workflow-core.json .workflow/implementation/implementation.json task-auth-001`
- `/04.5-validate-task-completion .workflow/core/workflow-core.json .workflow/implementation/implementation.json task-auth-001 strict`
- `/dt:workflow:05-architect-tests .workflow/core/workflow-core.json .workflow/implementation/implementation.json`
- `/dt:workflow:06-assure-quality .workflow/core/workflow-core.json .workflow/testing/testing.json`
- `/dt:workflow:07-create-pr .workflow/core/workflow-core.json`

## Error Handling

### Graceful Degradation

```bash
# Handle missing workflow files
handle_missing_file() {
    local file_path="$1"
    local file_description="$2"
    echo "${WARNING} $file_description not found: $file_path"
    echo "This indicates the corresponding workflow phase has not been completed."
}

# Handle corrupted JSON
handle_corrupted_json() {
    local file_path="$1"
    local file_description="$2"
    echo "${ERROR} $file_description contains invalid JSON: $file_path"
    echo "This file may need to be regenerated or manually corrected."
}

# Validate JSON files
validate_json_file() {
    local file_path="$1"
    if [[ -f "$file_path" ]]; then
        if ! jq empty "$file_path" 2>/dev/null; then
            return 1
        fi
    fi
    return 0
}
```

## Quality Assurance

### Validation Checks

1. **File Integrity**: Verify all workflow files contain valid JSON
2. **State Consistency**: Ensure current phase matches file completion status
3. **Dependency Validation**: Verify prerequisite phases are complete
4. **Task Consistency**: Ensure task states are logically consistent

### Progress Calculation

```bash
calculate_phase_progress() {
    local phase="$1"
    case "$phase" in
        "requirements_analysis")
            # Calculate based on requirements.json completeness
            ;;
        "architecture_design")
            # Calculate based on architecture.json completeness
            ;;
        "implementation_planning")
            # Calculate based on implementation.json completeness
            ;;
        "code_generation")
            # Calculate based on task completion status
            ;;
        "testing")
            # Calculate based on testing.json completeness
            ;;
        "quality_assurance")
            # Calculate based on quality metrics
            ;;
        "pull_request")
            # Calculate based on PR creation status
            ;;
    esac
}
```

## Integration with Modular Workflow System

### File Structure Compliance

```
.workflow/
├── core/
│   └── workflow-core.json          # Primary state tracking
├── context/
│   └── project-context.json        # Project discovery results
├── requirements/
│   └── requirements.json           # Requirements analysis
├── architecture/
│   └── architecture.json           # System design
├── implementation/
│   └── implementation.json         # Task planning and progress
├── testing/
│   └── testing.json                # Test architecture
└── execution/
    ├── validation-results.json     # Task validation outcomes
    └── failure-logs.json           # Error tracking
```

### State Synchronization

Ensure progress report reflects actual file states and maintains consistency with the modular workflow system used by commands 01-07.

---

**Chain Integration**: This utility command supports the main workflow chain (01-07) by providing comprehensive state analysis and next action determination. It does not modify workflow state but provides critical visibility into current progress and recommended next steps.

**Enterprise Quality**: Implements enterprise-grade progress tracking with detailed metrics, visual reporting, and fail-safe error handling to support complex development workflows.

## MANDATORY Next Command Display

This command MUST conclude by displaying the complete next recommended command with actual parameters (not placeholders), following the established pattern from all other workflow commands. The Chain of Thought analysis determines the appropriate next action based on comprehensive workflow state assessment.
