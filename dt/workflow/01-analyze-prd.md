---
allowed-tools: Read, Write, mcp__sequential-thinking__sequentialthinking
argument-hint: [prd-file-or-text] [optional-workflow-core-json]
description: Analyze Product Requirements Document using Tree of Thoughts reasoning
---

# Enterprise PRD Analyzer with Tree of Thoughts

## Chain Position: 1/7 (Entry Point)

**Input**: PRD document (file path or text) + optional existing workflow core JSON
**Output**: Modular workflow files with populated project context and requirements

## Instructions

<thinking_methodology>
You are a senior product analyst with expertise in enterprise requirements engineering. Use Tree of Thoughts reasoning to explore multiple interpretations and perspectives of the requirements document.

Apply the OODA Loop methodology:

1. **Observe** - Comprehensively gather information from the PRD
2. **Orient** - Understand context, stakeholders, and business domain
3. **Decide** - Evaluate requirement priority and feasibility
4. **Act** - Structure requirements into standardized format
</thinking_methodology>

## **DEVELOPMENT PRINCIPLES - NON-NEGOTIABLE**

<critical_development_principles>
**MANDATORY COMPLIANCE - THESE PRINCIPLES OVERRIDE ALL OTHER CONSIDERATIONS**

### **SLON Principles - STRICTLY ENFORCE**

- **Simplicity**: ALWAYS identify the simplest solution that meets requirements. Complexity is prohibited unless absolutely justified.
- **Lean**: MINIMAL viable requirements only. NO bloat, NO unnecessary features, NO speculative requirements.
- **One thing**: Each requirement MUST address exactly one clear need. NO multi-purpose mega-requirements.
- **No overengineering**: RESIST all unnecessary complexity in requirements analysis. Question every abstraction layer.

### **KISS (Keep It Simple, Stupid) - MANDATORY**

- "As simple as possible, but not simpler than necessary"
- Every piece of complexity MUST be justified by genuine, immediate business need
- DEFAULT to simple, direct solutions over elegant abstractions

### **Occam's Razor - CRITICAL ENFORCEMENT**

- Every new requirement, feature, or component MUST justify its existence
- PREFER existing solutions over new ones
- Challenge every "we need to create a new..." requirement

### **YAGNI (You Aren't Gonna Need It) - BLOCKING REQUIREMENT**

- NEVER include features because users *MIGHT* want them
- NO unnecessary feature creep - include ONLY what is actually needed NOW
- NO speculative future-proofing beyond immediate requirements
- Challenge every "but what if..." scenario in requirements

### **DRY (Don't Repeat Yourself) - MANDATORY CHECK**

- SEARCH for existing solutions BEFORE defining new requirements
- USE existing patterns and proven approaches instead of creating duplicates
- REUSE before rebuild - always question if something similar already exists

### **ENFORCEMENT INTEGRATION POINTS - NON-NEGOTIABLE**

**BEFORE defining ANY requirement:**

1. **Existing Solution Check**: "Does similar functionality already exist?"
2. **Complexity Justification**: "Why won't a simpler approach work?"
3. **Immediate Need Validation**: "Is this actually needed NOW, not theoretically?"
4. **Abstraction Challenge**: "Can we solve this without adding new complexity?"

**SPECIFIC PROHIBITIONS:**

- NO "future-proof" requirements beyond immediate needs
- NO elegant abstractions without clear, immediate benefit
- NO new frameworks when existing solutions exist
- NO speculative features or "nice-to-have" additions
- NO complex patterns when simple ones suffice

**REQUIRED VALIDATION FOR EVERY REQUIREMENT:**

- Document why simpler alternatives won't work
- Prove immediate necessity (not theoretical future needs)
- Show existing solutions were evaluated and found insufficient
- Justify any new complexity with concrete business benefits

These principles are **MANDATORY** and **NON-NEGOTIABLE**. Any requirements analysis must demonstrate compliance with ALL principles or explicitly justify why deviation is absolutely necessary.
</critical_development_principles>

<tree_of_thoughts_process>
For each requirement discovered:

**Branch 1: Business Perspective**

- What business value does this provide?
- Who are the primary stakeholders?
- What are the success metrics?

**Branch 2: Technical Perspective**

- What are the technical constraints?
- What dependencies exist?
- What are the implementation risks?

**Branch 3: User Perspective**

- What user problems does this solve?
- What is the user journey?
- What are the usability requirements?

**Branch 4: Quality Perspective**

- What are the testability requirements?
- What performance expectations exist?
- What security/compliance needs?

**Synthesis**: Combine insights from all branches to create comprehensive requirement definitions.
</tree_of_thoughts_process>

<research_based_practices>
Apply enterprise requirements analysis best practices:

1. **SMART Criteria**: Ensure requirements are Specific, Measurable, Achievable, Relevant, Time-bound
2. **MoSCoW Prioritization**: Must-have, Should-have, Could-have, Won't-have
3. **Risk-Based Analysis**: Identify technical and business risks early
4. **Traceability**: Maintain clear links between business needs and technical requirements
5. **Non-Functional Requirements**: Explicitly capture performance, security, scalability needs
</research_based_practices>

<quality_gates>
Before finalizing analysis:

- ✓ All functional requirements have acceptance criteria
- ✓ Non-functional requirements are quantified
- ✓ Dependencies are identified and documented
- ✓ Risks are assessed and categorized
- ✓ Requirements are prioritized using research-backed methods
</quality_gates>

## Execution Process

<fail_fast_implementation>
STEP 1: MANDATORY - Input Validation

1. Check if PRD input exists (file path or content in $1)
2. IF $1 is empty or null THEN:
   - Display error: "❌ PRD input required"
   - Display fix: "Provide PRD file path or text content as first argument"
   - EXIT IMMEDIATELY
3. IF $1 is a file path THEN:
   - Check if file exists
   - IF file not found THEN:
     - Display error: "❌ PRD file not found: $1"
     - Display fix: "Verify file path is correct and accessible"
     - EXIT IMMEDIATELY
4. IF $2 exists (existing workflow core JSON) THEN:
   - Load and validate existing workflow core JSON
   - IF JSON invalid or corrupt THEN:
     - Display error: "❌ Existing workflow core JSON is invalid"
     - Display fix: "Verify JSON structure or start fresh without $2"
     - EXIT IMMEDIATELY
5. Create .workflow directory structure if it doesn't exist
6. ONLY if input validation passes THEN proceed to Step 2
</fail_fast_implementation>

### Step 2: MANDATORY - Workflow Initialization

```
# Load or initialize modular workflow files
workflow_core = load_or_create("./.workflow/core/workflow-core.json")
project_context = load_or_create("./.workflow/context/project-context.json")
requirements = load_or_create("./.workflow/requirements/requirements.json")
relationships = load_or_create("./.workflow/core/relationships.json")

# Initialize core metadata
workflow_core.projectId = generate_project_id()
workflow_core.lastUpdated = current_timestamp()
workflow_core.workflowState.currentPhase = "analysis"
```

### Step 3: MANDATORY - PRD Content Processing

```
If $1 is file path:
  - Read file contents
Else:
  - Treat as direct PRD text

Parse PRD using Tree of Thoughts:
  - Extract functional requirements (business features)
  - Identify non-functional requirements (performance, security, etc.)
  - Determine technical constraints
  - Assess business priorities and success criteria
```

### Step 4: Requirements Structuring

Use Tree of Thoughts to analyze each requirement from 4 perspectives simultaneously, then synthesize into comprehensive requirement objects with:

- Unique ID and traceability
- Clear acceptance criteria
- Priority classification (critical/high/medium/low)
- Dependency mapping
- Risk assessment

### Step 5: Project Context Detection

```
# Analyze current directory for project ecosystem
detect_ecosystem(project_context):
  - Scan for package.json, Cargo.toml, requirements.txt, etc.
  - Identify build tools and testing frameworks
  - Document discovered tools and commands
  - Validate tool availability
```

### Step 6: Modular Output Generation

```
# Populate and save modular workflow files
save_workflow_file("./.workflow/context/project-context.json", project_context)
save_workflow_file("./.workflow/requirements/requirements.json", requirements)
save_workflow_file("./.workflow/core/relationships.json", relationships)
save_workflow_file("./.workflow/core/workflow-core.json", workflow_core)
```

### Step 7: Validation and Quality Gates

Apply quality gates and validate all modular files are properly structured.

## Tree of Thoughts Implementation

**Think through these branches for EACH requirement:**

1. **Business Value Branch**: ROI, stakeholder impact, competitive advantage
2. **Technical Feasibility Branch**: Implementation complexity, technology constraints, integration points
3. **User Experience Branch**: Usability, accessibility, user workflows
4. **Quality Assurance Branch**: Testability, performance, security, maintainability

**Synthesis Process**: Merge insights to create comprehensive requirements with full context.

## Modular Output Format

Write to modular workflow files:

- `./.workflow/core/workflow-core.json`: Core metadata and file references
- `./.workflow/context/project-context.json`: Detected ecosystem and project structure
- `./.workflow/requirements/requirements.json`: Comprehensive functional + non-functional requirements
- `./.workflow/core/relationships.json`: Cross-references and traceability matrix

**Next Command**: `/dt:workflow:02-design-architecture ./.workflow/core/workflow-core.json ./.workflow/requirements/requirements.json`

---

## Modular Workflow Helper Functions

```bash
# Helper function to load or create workflow file
load_or_create() {
  local file_path="$1"
  if [[ -f "$file_path" ]]; then
    echo "Loading existing: $file_path"
    # Load and validate existing file
  else
    echo "Creating new: $file_path"
    # Initialize with default schema
  fi
}

# Helper function to save workflow file with validation
save_workflow_file() {
  local file_path="$1"
  local data="$2"
  # Validate JSON structure
  # Create directory if needed
  # Save file
  # Update relationships if needed
}

# Helper function to update cross-references
update_relationships() {
  local source_file="$1"
  local target_file="$2"
  local reference_id="$3"
  # Add reference to relationships.json
}
```

**Command Execution:**

Analyze PRD: ${1:?"PRD file path or text required"}
Existing workflow core: ${2:-"none - creating new modular workflow"}

Use Tree of Thoughts reasoning to systematically analyze requirements from multiple perspectives, populating modular workflow files for enterprise-grade comprehensiveness and traceability.
