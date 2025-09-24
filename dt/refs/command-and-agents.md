# Claude Code Commands & Sub-Agents: AI Implementation Reference

## Table of Contents

1. [Quick Reference & Decision Trees](#quick-reference--decision-trees)
2. [Slash Commands Implementation](#slash-commands-implementation)
3. [Sub-Agents Design & Prompt Engineering](#sub-agents-design--prompt-engineering)
4. [Hooks & Event-Driven Architecture](#hooks--event-driven-architecture)
5. [Advanced Patterns & Workflows](#advanced-patterns--workflows)
6. [Template Library](#template-library)
7. [Troubleshooting & Validation](#troubleshooting--validation)

---

## Quick Reference & Decision Trees

### When to Create What

**Create a Slash Command when:**

- User needs a repeatable action with specific arguments
- Task involves executing bash commands or file operations
- Workflow needs user confirmation or input validation
- You need standardized project-specific operations

**Create a Sub-Agent when:**

- Task requires specialized expertise or domain knowledge
- Complex multi-step reasoning is needed
- Different tool access patterns are required
- You need focused, context-specific AI assistance

**Create a Hook when:**

- You need to validate or modify tool usage
- Workflow requires automatic pre/post-processing
- Security validation is needed
- Integration between different components is required

### File Locations

```
Project Level:
├── .claude/
│   ├── commands/          # Slash commands
│   ├── agents/           # Sub-agents
│   └── settings.json     # Hooks configuration

User Level:
├── ~/.claude/
│   ├── commands/         # Personal commands
│   └── agents/          # Personal agents
```

---

## Slash Commands Implementation

### Basic Structure

Slash commands are markdown files with YAML frontmatter:

```markdown
---
allowed-tools: Tool1, Tool2
argument-hint: [description of expected arguments]
description: Brief command explanation
---

Command instructions and prompt content here.
Use $ARGUMENTS for all arguments or $1, $2 for specific ones.
```

### Core Configuration Options

**allowed-tools:** Control tool access for security

- `Bash(git add:*)` - Allow git add with any arguments
- `Read, Write, Edit` - Allow file operations
- `*` - Allow all tools (use cautiously)

**argument-hint:** Guide users on expected input

- `[commit message]` - Single argument
- `[component-name] [path]` - Multiple arguments
- `[optional-flag] message` - Mixed optional/required

### Argument Handling Patterns

#### Single Argument Pattern

```markdown
---
argument-hint: [commit message]
---

Create a git commit with message: $ARGUMENTS
```

#### Multiple Arguments Pattern

```markdown
---
argument-hint: [component-name] [optional-path]
---

Create React component named $1.
Path: ${2:-"src/components"}
```

#### Validation Pattern

```markdown
---
argument-hint: [branch-name]
---

<validation>
- Ensure branch name follows naming convention
- Check if branch already exists
- Validate user has necessary permissions
</validation>

Create and switch to branch: $ARGUMENTS
```

### Security Best Practices

**Tool Restrictions:**

```markdown
---
allowed-tools: Bash(git add:*), Bash(git commit:*), Read
---
```

**Input Validation:**

```markdown
Before proceeding:
1. Validate all file paths are within project directory
2. Sanitize user input to prevent injection
3. Confirm destructive operations with user
```

### Real-World Command Examples

#### Git Commit Command

```markdown
---
allowed-tools: Bash(git add:*), Bash(git commit:*), Bash(git status:*)
argument-hint: [commit message]
description: Create structured git commit with validation
---

<instructions>
1. Run git status to show current changes
2. Validate commit message follows project conventions
3. ALWAYS ask for user confirmation before committing
4. Only commit staged changes, never auto-stage files
</instructions>

<commit_rules>
- Use format: [scope] lowercase description
- Be concise but descriptive
- No trailing periods
</commit_rules>

Create git commit with message: $ARGUMENTS
```

#### React Component Generator

```markdown
---
allowed-tools: Write, Read, Glob
argument-hint: [ComponentName] [optional-props-type]
description: Generate TypeScript React component
---

<component_generation>
1. Validate ComponentName is PascalCase
2. Default path: "src/components"
3. Props types: none, ChildrenProps, ClassNameProps, custom
4. Follow project TypeScript conventions
5. No aria-* attributes per project rules
</component_generation>

Generate React component: $1
Props configuration: ${2:-"none"}
```

---

## Sub-Agents Design & Prompt Engineering

### Architecture Principles

Sub-agents are specialized AI assistants with:

- **Separate context window** - Clean slate for focused work
- **Domain expertise** - Specific knowledge and skills
- **Tool access control** - Security and efficiency
- **Coordinated workflows** - Work with other agents

### File Structure

```markdown
---
name: agent-name
description: When this agent should be invoked
tools: tool1, tool2  # Optional
model: sonnet  # Optional
---

<role_definition>
You are a [specific expertise] specialist with deep knowledge of [domain].
Your core responsibilities include:
- [Primary responsibility 1]
- [Primary responsibility 2]
- [Primary responsibility 3]
</role_definition>

<capabilities>
- [Specific skill 1]
- [Specific skill 2]
- [Specific skill 3]
</capabilities>

<methodology>
When approaching tasks:
1. [Step 1 methodology]
2. [Step 2 methodology]
3. [Step 3 methodology]
</methodology>

[Additional specialized instructions]
```

### Role Definition Techniques

#### Expertise-Based Definition

```markdown
---
name: security-auditor
description: Security analysis and vulnerability assessment
tools: Read, Grep, Bash
model: opus
---

<role_definition>
You are a cybersecurity expert specializing in application security auditing.
You have deep expertise in:
- OWASP Top 10 vulnerabilities
- Static code analysis
- Dependency vulnerability assessment
- Security best practices implementation
</role_definition>
```

#### Process-Based Definition

```markdown
---
name: code-reviewer
description: Comprehensive code quality review
tools: Read, Grep, Diff
model: sonnet
---

<role_definition>
You are a senior software engineer focused on code quality and maintainability.
Your review process follows a systematic approach:
1. Architecture and design pattern analysis
2. Code quality and style assessment
3. Performance and security considerations
4. Testing coverage and quality evaluation
</role_definition>
```

### Model Selection Strategy

**Haiku (Fast, Simple Tasks):**

- File formatting and simple transformations
- Basic validation and checks
- Quick analysis tasks
- Template generation

**Sonnet (Standard Development):**

- Code generation and modification
- Testing and debugging
- Documentation creation
- Standard development workflows

**Opus (Complex Reasoning):**

- Architecture design and analysis
- Security auditing
- Complex problem solving
- Strategic planning and coordination

### Tool Access Patterns

#### Minimal Access (Security-First)

```markdown
---
tools: Read
---
```

#### Read-Only Analysis

```markdown
---
tools: Read, Grep, Glob
---
```

#### Development Workflow

```markdown
---
tools: Read, Write, Edit, Bash
---
```

#### Full Access (Use Cautiously)

```markdown
---
# tools: (inherit all - default)
---
```

### Advanced Prompt Engineering

#### Structured Thinking Pattern

```markdown
<thinking_process>
When analyzing complex problems:
1. **Observe** - Gather comprehensive information
2. **Orient** - Understand context and constraints
3. **Decide** - Evaluate options and choose approach
4. **Act** - Implement solution with verification
</thinking_process>

<verification>
After each major step:
- Verify assumptions are still valid
- Check for unintended consequences
- Validate output meets requirements
</verification>
```

#### Multi-Agent Coordination

```markdown
<coordination_rules>
When working with other agents:
- Provide clear, specific instructions
- Define expected output format
- Share relevant context and constraints
- Avoid duplicating efforts
- Synthesize results when complete
</coordination_rules>
```

### Sub-Agent Templates

#### Research Agent

```markdown
---
name: research-specialist
description: Comprehensive research and information gathering
tools: WebSearch, WebFetch, Read, Grep
model: sonnet
---

<role_definition>
You are a research specialist skilled in systematic information gathering and analysis.
</role_definition>

<methodology>
Research Process (OODA Loop):
1. **Observe** - Identify information gaps and sources
2. **Orient** - Understand context and prioritize queries
3. **Decide** - Choose most effective research strategies
4. **Act** - Execute searches and gather information
</methodology>

<source_evaluation>
Prioritize sources by:
- Authority and credibility
- Recency and relevance
- Depth and accuracy
- Verifiability
</source_evaluation>

<output_format>
Provide research findings in structured format:
- Executive summary
- Key findings with sources
- Detailed analysis
- Recommendations
</output_format>
```

#### Backend Architect

```markdown
---
name: backend-architect
description: Backend system design and architecture
tools: Read, Write, Glob, Grep
model: opus
---

<role_definition>
You are a senior backend architect with expertise in scalable system design.
Your specializations include:
- Microservice architecture patterns
- Database design and optimization
- API design and integration
- Performance and scalability
- Security and compliance
</role_definition>

<design_principles>
Follow these architectural principles:
- Domain-driven design
- SOLID principles
- Microservice best practices
- Security by design
- Performance optimization
</design_principles>

<methodology>
Architecture Process:
1. **Requirements Analysis** - Understand functional and non-functional requirements
2. **System Design** - Create high-level architecture
3. **Component Design** - Detail individual components
4. **Integration Planning** - Define service interactions
5. **Validation** - Review against requirements and constraints
</methodology>
```

---

## Hooks & Event-Driven Architecture

### Hook Configuration

Hooks are configured in `.claude/settings.json`:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash.*",
        "hooks": [
          {
            "type": "command",
            "command": "python validate_bash.py"
          }
        ]
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Write.*",
        "hooks": [
          {
            "type": "command",
            "command": "eslint --fix $CLAUDE_TOOL_ARGS"
          }
        ]
      }
    ]
  }
}
```

### Event Types

**PreToolUse:** Validate before tool execution

- Security validation
- Input sanitization
- Permission checks
- Environment validation

**PostToolUse:** Process after successful execution

- Code formatting
- Quality checks
- Automated testing
- Notification systems

**UserPromptSubmit:** React to user input

- Context validation
- Automatic project setup
- Workflow initiation

**Stop/SubagentStop:** Cleanup and finalization

- Resource cleanup
- Status reporting
- Result validation

### Security Patterns

#### Input Validation Hook

```python
#!/usr/bin/env python3
import sys
import json
import re

def validate_bash_command(command):
    """Validate bash commands for security"""
    dangerous_patterns = [
        r'rm\s+-rf\s+/',
        r'sudo\s+rm',
        r'>\s*/dev/sd[a-z]',
        r'dd\s+if=',
        r'mkfs\.',
        r'fdisk',
        r'eval\s+\$',
        r'curl.*\|\s*sh',
    ]

    issues = []
    for pattern in dangerous_patterns:
        if re.search(pattern, command, re.IGNORECASE):
            issues.append(f"Potentially dangerous pattern: {pattern}")

    return issues

if __name__ == "__main__":
    tool_args = os.environ.get('CLAUDE_TOOL_ARGS', '')
    issues = validate_bash_command(tool_args)

    if issues:
        result = {
            "block": True,
            "message": "Security validation failed",
            "issues": issues
        }
        print(json.dumps(result))
        sys.exit(2)  # Block execution

    sys.exit(0)  # Allow execution
```

#### File Access Control

```bash
#!/bin/bash
# Validate file operations stay within project boundaries

PROJECT_DIR="${CLAUDE_PROJECT_DIR}"
REQUESTED_PATH="$1"

# Resolve absolute path
RESOLVED_PATH=$(realpath "$REQUESTED_PATH" 2>/dev/null)

# Check if path is within project directory
if [[ ! "$RESOLVED_PATH" =~ ^"$PROJECT_DIR" ]]; then
    echo '{"block": true, "message": "File access outside project directory denied"}'
    exit 2
fi

exit 0
```

### Integration Patterns

#### Command + Hook Integration

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash.*git commit.*",
        "hooks": [
          {
            "type": "command",
            "command": "python check_commit_rules.py"
          }
        ]
      }
    ]
  }
}
```

#### Agent + Hook Coordination

```markdown
---
name: secure-developer
description: Development with automatic security validation
tools: Write, Edit, Bash
---

<security_integration>
This agent works with security hooks to:
- Validate all file operations
- Check code against security patterns
- Ensure compliance with project policies
</security_integration>

All code changes will be automatically validated by security hooks.
```

---

## Advanced Patterns & Workflows

### Multi-Agent Workflows

#### Research Lead + Subagent Pattern

```markdown
# Research Lead Agent
---
name: research-lead
description: Coordinate complex research projects
tools: Task
model: opus
---

<coordination_strategy>
For complex research:
1. Break down into focused sub-topics
2. Create specialized subagents for each area
3. Provide detailed instructions and context
4. Synthesize findings into comprehensive report
</coordination_strategy>

<subagent_creation>
Create subagents with:
- Specific research objectives
- Expected output format
- Relevant context and constraints
- Reliable source recommendations
</subagent_creation>
```

#### Code Review Pipeline

```markdown
# Security Reviewer
---
name: security-reviewer
description: Security-focused code review
tools: Read, Grep, Bash
model: opus
---

Focus on security vulnerabilities, authentication flaws, and data protection.

# Performance Reviewer
---
name: performance-reviewer
description: Performance and optimization review
tools: Read, Grep, Bash
model: sonnet
---

Analyze performance bottlenecks, memory usage, and optimization opportunities.

# Style Reviewer
---
name: style-reviewer
description: Code style and maintainability review
tools: Read, Grep
model: haiku
---

Check coding standards, documentation, and maintainability patterns.
```

### Workflow Orchestration

#### Command + Agent Workflow

```markdown
---
allowed-tools: Task
argument-hint: [feature-description]
description: Complete feature development workflow
---

<workflow>
1. Use architecture-agent to design feature
2. Use code-generator-agent to implement
3. Use test-agent to create comprehensive tests
4. Use review-agent to validate implementation
5. Create documentation with docs-agent
</workflow>

Implement feature: $ARGUMENTS
```

#### Progressive Enhancement

```markdown
---
name: progressive-enhancer
description: Incrementally improve codebase
tools: Read, Write, Edit, Task
model: sonnet
---

<enhancement_strategy>
1. **Analyze** current code quality and patterns
2. **Prioritize** improvements by impact and effort
3. **Implement** changes incrementally
4. **Validate** each improvement independently
5. **Document** changes and rationale
</enhancement_strategy>
```

### Performance Optimization

#### Parallel Tool Execution

```markdown
<efficiency>
Use parallel tool calls when possible:
- Read multiple files simultaneously
- Run independent bash commands in parallel
- Gather information from multiple sources concurrently
</efficiency>

Example: Read([file1, file2, file3]) rather than sequential reads.
```

#### Context Management

```markdown
<context_optimization>
- Limit tool output to relevant information only
- Use specific grep patterns rather than reading entire files
- Focus subagent instructions on specific outcomes
- Minimize unnecessary tool invocations
</context_optimization>
```

---

## Template Library

### Essential Command Templates

#### Git Workflow Commands

```markdown
# Commit Command
---
allowed-tools: Bash(git add:*), Bash(git commit:*), Bash(git status:*)
argument-hint: [commit message]
description: Create structured git commit
---

<validation>
1. Check git status
2. Validate commit message format
3. Confirm with user before committing
</validation>

# Branch Command
---
allowed-tools: Bash(git checkout:*), Bash(git branch:*)
argument-hint: [branch-name]
description: Create and switch to new branch
---

<branch_rules>
- Use kebab-case naming
- Include ticket number if applicable
- Validate branch doesn't exist
</branch_rules>

# Deploy Command
---
allowed-tools: Bash
argument-hint: [environment]
description: Deploy to specified environment
---

<deployment_safety>
1. Validate environment exists
2. Check for uncommitted changes
3. Run tests before deployment
4. Confirm deployment with user
</deployment_safety>
```

#### Code Generation Commands

```markdown
# React Component
---
allowed-tools: Write, Read, Glob
argument-hint: [ComponentName] [props-type]
description: Generate TypeScript React component
---

<generation_rules>
- PascalCase component names
- TypeScript interfaces for props
- Follow project structure conventions
- Include basic styling setup
</generation_rules>

# API Endpoint
---
allowed-tools: Write, Read, Glob, Edit
argument-hint: [endpoint-name] [method]
description: Generate API endpoint with validation
---

<api_patterns>
- RESTful conventions
- Input validation
- Error handling
- Type safety
- Documentation
</api_patterns>

# Database Migration
---
allowed-tools: Write, Bash
argument-hint: [migration-name]
description: Create database migration
---

<migration_safety>
- Reversible migrations only
- Data preservation checks
- Index considerations
- Performance impact analysis
</migration_safety>
```

### Essential Agent Templates

#### Development Agents

```markdown
# Full-Stack Developer
---
name: fullstack-developer
description: Complete application development
tools: Read, Write, Edit, Bash
model: sonnet
---

<expertise>
- Frontend: React, TypeScript, CSS
- Backend: Node.js, Python, databases
- DevOps: Docker, CI/CD, deployment
- Testing: Unit, integration, e2e
</expertise>

# DevOps Engineer
---
name: devops-engineer
description: Infrastructure and deployment automation
tools: Read, Write, Bash, WebFetch
model: sonnet
---

<specializations>
- Container orchestration
- CI/CD pipeline design
- Infrastructure as code
- Monitoring and observability
- Security and compliance
</specializations>

# QA Engineer
---
name: qa-engineer
description: Comprehensive testing and quality assurance
tools: Read, Write, Bash
model: sonnet
---

<testing_approach>
- Test strategy development
- Automated test creation
- Manual testing procedures
- Performance testing
- Security testing
</testing_approach>
```

#### Specialized Agents

```markdown
# Data Analyst
---
name: data-analyst
description: Data analysis and visualization
tools: Read, Write, ExecuteCode
model: sonnet
---

<analytical_skills>
- Statistical analysis
- Data visualization
- Pattern recognition
- Predictive modeling
- Report generation
</analytical_skills>

# Technical Writer
---
name: technical-writer
description: Documentation and communication
tools: Read, Write, WebFetch
model: haiku
---

<documentation_types>
- API documentation
- User guides
- Architecture decisions
- Process documentation
- Training materials
</documentation_types>

# Security Analyst
---
name: security-analyst
description: Security assessment and hardening
tools: Read, Grep, Bash
model: opus
---

<security_domains>
- Vulnerability assessment
- Penetration testing
- Security architecture review
- Compliance validation
- Incident response
</security_domains>
```

---

## Troubleshooting & Validation

### Common Issues and Solutions

#### Command Issues

**Problem:** Command not found or not executing

```markdown
Troubleshooting Steps:
1. Check file location (.claude/commands/)
2. Verify YAML frontmatter syntax
3. Validate markdown format
4. Check tool permissions
5. Test argument parsing
```

**Problem:** Tool permission errors

```markdown
Solutions:
- Verify allowed-tools configuration
- Check specific tool syntax
- Validate argument patterns
- Review security restrictions
```

#### Agent Issues

**Problem:** Agent not being invoked

```markdown
Troubleshooting Steps:
1. Check agent description clarity
2. Verify file naming conventions
3. Test manual invocation
4. Review tool access configuration
5. Validate YAML syntax
```

**Problem:** Poor agent performance

```markdown
Optimization Steps:
- Refine role definition
- Improve prompt specificity
- Adjust model selection
- Optimize tool access
- Add structured thinking patterns
```

#### Hook Issues

**Problem:** Hooks not triggering

```markdown
Debugging Steps:
1. Verify settings.json syntax
2. Check matcher patterns
3. Test hook commands manually
4. Review event types
5. Validate file permissions
```

### Validation Checklists

#### Command Validation

```markdown
✓ YAML frontmatter is valid
✓ All required fields present
✓ Tool permissions are appropriate
✓ Argument handling is correct
✓ Error cases are handled
✓ Security considerations addressed
✓ User confirmation for destructive operations
✓ Clear description and hints provided
```

#### Agent Validation

```markdown
✓ Role definition is specific and clear
✓ Capabilities are well-defined
✓ Tool access is appropriate
✓ Model selection is optimal
✓ Prompt engineering follows best practices
✓ Structured thinking patterns included
✓ Integration with other agents considered
✓ Performance characteristics are acceptable
```

#### Hook Validation

```markdown
✓ Matcher patterns are accurate
✓ Hook commands are tested
✓ Security implications reviewed
✓ Error handling is robust
✓ Performance impact is minimal
✓ Integration points are validated
✓ Documentation is complete
✓ Rollback procedures exist
```

### Testing Strategies

#### Integration Testing

```bash
# Test command execution
claude /test-command "test arguments"

# Test agent invocation
claude "Use the test-agent to analyze this file"

# Test hook triggers
claude --debug "Perform action that triggers hooks"
```

#### Validation Scripts

```python
#!/usr/bin/env python3
"""Validate Claude Code configuration"""

import yaml
import json
import os
from pathlib import Path

def validate_commands():
    """Validate all command files"""
    commands_dir = Path(".claude/commands")
    for cmd_file in commands_dir.glob("*.md"):
        with open(cmd_file) as f:
            content = f.read()
            # Validate YAML frontmatter
            # Validate markdown structure
            # Check tool permissions

def validate_agents():
    """Validate all agent files"""
    agents_dir = Path(".claude/agents")
    for agent_file in agents_dir.glob("*.md"):
        with open(agent_file) as f:
            content = f.read()
            # Validate YAML frontmatter
            # Check role definitions
            # Validate tool access

def validate_hooks():
    """Validate hooks configuration"""
    settings_file = Path(".claude/settings.json")
    if settings_file.exists():
        with open(settings_file) as f:
            config = json.load(f)
            # Validate hook configuration
            # Check matcher patterns
            # Validate commands exist

if __name__ == "__main__":
    validate_commands()
    validate_agents()
    validate_hooks()
```

---

## Best Practices Summary

### For AI Models Creating Claude Code Extensions

1. **Start Simple**: Begin with basic functionality, then enhance
2. **Be Explicit**: Clear instructions prevent ambiguity
3. **Security First**: Always validate inputs and restrict tools appropriately
4. **User Experience**: Provide clear hints, descriptions, and confirmations
5. **Maintainability**: Use consistent patterns and good documentation
6. **Performance**: Optimize for efficiency and minimal context usage
7. **Integration**: Consider how components work together
8. **Validation**: Always test and validate functionality

### Key Principles

- **Specificity over Generality**: Focused tools are more effective
- **Security by Design**: Build in protections from the start
- **User-Centric Design**: Optimize for developer experience
- **Composability**: Design components that work well together
- **Maintainability**: Write code that's easy to understand and modify

This reference provides the foundation for creating effective Claude Code extensions. Use it as both a learning resource and a quick reference during development.
