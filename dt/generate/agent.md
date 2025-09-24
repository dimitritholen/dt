---
allowed-tools: Read, Write, Task
argument-hint: [agent-description]
description: Generate a Claude Code agent following documentation best practices
---

Generate a new Claude Code sub-agent following all documentation best practices.

## **DEVELOPMENT PRINCIPLES - NON-NEGOTIABLE**

<critical_development_principles>
**MANDATORY COMPLIANCE - THESE PRINCIPLES OVERRIDE ALL OTHER CONSIDERATIONS**

### **SLON Principles - STRICTLY ENFORCE**

- **Simplicity**: ALWAYS create the simplest agent that solves the specific need. Complexity is prohibited unless absolutely justified.
- **Lean**: MINIMAL viable agent capabilities only. NO bloat, NO unnecessary features, NO speculative functionality.
- **One thing**: Each agent MUST do exactly one clear thing well. NO multi-purpose mega-agents.
- **No overengineering**: RESIST all unnecessary complexity in agent design. Question every abstraction layer.

### **KISS (Keep It Simple, Stupid) - MANDATORY**

- "As simple as possible, but not simpler than necessary"
- Every piece of agent complexity MUST be justified by genuine, immediate need
- DEFAULT to simple, direct agent approaches over elegant abstractions

### **Occam's Razor - CRITICAL ENFORCEMENT**

- Every new agent capability, tool, or feature MUST justify its existence
- PREFER existing agents over new ones
- Challenge every "we need to create a new agent..." decision

### **YAGNI (You Aren't Gonna Need It) - BLOCKING REQUIREMENT**

- NEVER add agent features because the user *MIGHT* want them
- NO unnecessary feature creep - include ONLY what is actually needed NOW
- NO speculative future-proofing beyond immediate requirements
- Challenge every "but what if..." agent scenario

### **DRY (Don't Repeat Yourself) - MANDATORY CHECK**

- SEARCH existing agents for similar functionality BEFORE creating new agents
- USE existing agent patterns instead of creating duplicates
- REUSE before rebuild - always question if a similar agent already exists

**BEFORE creating ANY new agent:**

1. **Existing Agent Check**: "Does a similar agent already exist?"
2. **Complexity Justification**: "Why won't a simpler agent work?"
3. **Immediate Need Validation**: "Is this agent actually needed NOW, not theoretically?"
4. **Abstraction Challenge**: "Can we solve this without creating a new agent?"

These principles are **MANDATORY** and **NON-NEGOTIABLE**. Any new agent must demonstrate compliance with ALL principles or explicitly justify why deviation is absolutely necessary.
</critical_development_principles>

<instructions>
1. Validate input description for agent purpose
2. Read ~/.claude/dt/refs/command-and-agents.md for agent best practices
3. Use Chain of Thought analysis via Task tool
4. Generate properly structured agent with role definitions
5. Save to ~/.claude/agents/ with appropriate name
6. Review generated agent for compliance
</instructions>

**Step 1: Input Validation**

Check if agent description is provided: "$ARGUMENTS"

If empty or unclear, show usage and stop:

- Usage: `/generate-agent "description of what the agent should specialize in"`
- Examples:
  - "Python backend development with security focus"
  - "React frontend components with TypeScript"
  - "DevOps automation and infrastructure management"
  - "Code review with performance optimization"
  - "Security auditing and vulnerability assessment"

**Step 2: Read Documentation**

Read ~/.claude/dt/refs/command-and-agents.md to understand agent best practices:

- Agent YAML frontmatter structure (name, description, tools, model)
- Role definition techniques (expertise-based vs process-based)
- Model selection strategy (haiku/sonnet/opus)
- Tool access patterns (minimal/read-only/development/full)
- Advanced prompt engineering patterns
- Agent validation requirements

**Step 3: Chain of Thought Analysis**

Use Task tool to analyze agent requirements for "$ARGUMENTS":

Create a specialist analysis to determine:

1. **Domain Expertise**: What specific knowledge area does this agent cover?
2. **Agent Type Classification**: Developer, Reviewer, Analyst, or Specialist?
3. **Required Tools**: What minimal tools are needed for this specialization?
4. **Model Selection**: Haiku (simple), Sonnet (standard), or Opus (complex)?
5. **Role Definition**: Expertise-based or process-based approach?
6. **Prompt Engineering Pattern**: CoT, Extended Thinking, or Multi-Agent coordination?
7. **Agent Naming**: Semantic precision naming (domain-role-specialization)

**Step 4: Generate Agent Structure**

Based on analysis results, create complete agent with:

**YAML Frontmatter:**

- name: Semantic precision naming (e.g., python-backend-architect)
- description: Clear trigger description with examples
- tools: Minimal required tools for security
- model: Appropriate model selection

**Agent Body:**

- Role definition with specific expertise
- Core responsibilities with methodology
- Capabilities section
- Quality standards and requirements
- Advanced patterns and techniques
- Structured thinking processes

**Step 5: Save Agent File**

Generate appropriate filename from description (kebab-case) and save to ~/.claude/agents/[agent-name].md

**Step 6: Code Review**

Validate the generated agent against documentation checklist:

- YAML syntax is valid
- All required fields present (name, description)
- Tool access is appropriate for specialization
- Model selection is optimal
- Role definition is specific and clear
- Capabilities are well-defined
- Methodology follows structured thinking patterns
- Integration with other agents considered
- Performance characteristics are acceptable

Present final agent location and confirm successful generation.
