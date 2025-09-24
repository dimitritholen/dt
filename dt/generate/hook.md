---
allowed-tools: Read, Write, Task
argument-hint: [hook-description]
description: Generate Claude Code hooks following documentation best practices
---

Generate new Claude Code hooks configuration following all documentation best practices.

<instructions>
1. Validate input description for hook purpose
2. Read ~/.claude/dt/refs/command-and-agents.md for hook patterns and security practices
3. Use Chain of Thought analysis via Task tool
4. Generate properly structured hook configuration
5. Save/update .claude/settings.json with appropriate hooks
6. Review generated hooks for compliance and security
</instructions>

**Step 1: Input Validation**

Check if hook description is provided: "$ARGUMENTS"

If empty or unclear, show usage and stop:

- Usage: `/generate-hook "description of what the hook should do"`
- Examples:
  - "validate bash commands for security before execution"
  - "auto-format code files after write operations"
  - "check file permissions before any file access"
  - "run tests after code generation"
  - "validate git commits meet project standards"

**Step 2: Read Documentation**

Read ~/.claude/dt/refs/command-and-agents.md to understand hook best practices:

- Hook types and event patterns (PreToolUse, PostToolUse, UserPromptSubmit, Stop/SubagentStop)
- Security validation patterns and examples
- Matcher pattern syntax and effectiveness
- Hook command structures and error handling
- Integration with existing commands and agents
- Performance considerations and minimal overhead

**Step 3: Chain of Thought Analysis**

Use Task tool to analyze hook requirements for "$ARGUMENTS":

Create a specialist analysis agent to determine:

1. **Hook Type Classification**: Which event type (PreToolUse, PostToolUse, UserPromptSubmit, Stop/SubagentStop) based on purpose
2. **Security Requirements**: What validation, sanitization, or permission checks are needed
3. **Matcher Patterns**: Precise regex patterns to match relevant tool usage or contexts
4. **Hook Commands**: What scripts, commands, or validation should execute
5. **Script Generation Needs**: Whether to create Python/Bash validation scripts
6. **Error Handling Strategy**: How hooks should fail (block vs warn vs log)
7. **Integration Points**: How hooks work with existing commands, agents, and workflows
8. **Performance Impact**: Ensuring minimal overhead and fast execution

**Step 4: Generate Hook Configuration**

Based on analysis results, create complete hook configuration with:

**JSON Structure:**

- Proper event type classification
- Accurate matcher patterns with regex validation
- Appropriate hook commands (scripts or built-in)
- Error handling and response patterns
- Integration with existing configurations

**Security Scripts (if needed):**

- Python validation scripts for complex logic
- Bash scripts for file system operations
- Input sanitization and boundary checking
- Permission validation and safety checks

**Configuration Elements:**

- Event type specification
- Matcher pattern optimization
- Command execution strategy
- Error response configuration
- Integration documentation

**Step 5: Save/Update Hook Configuration**

Handle .claude/settings.json file operations:

1. **Read Existing Configuration**: Check if .claude/settings.json exists
2. **Merge Strategy**: Intelligently merge new hooks with existing ones
3. **Validation**: Ensure JSON syntax and structure validity
4. **Backup**: Create backup of existing configuration before changes
5. **Script Placement**: Save any generated validation scripts to appropriate locations
6. **Permissions**: Set correct file permissions for security scripts

**Step 6: Validation and Review**

Validate the generated hook configuration against documentation checklist:

- JSON syntax is valid and well-formed
- All required fields present and correctly formatted
- Matcher patterns are accurate and tested
- Hook commands exist and are executable
- Security implications reviewed and addressed
- Error handling is robust and appropriate
- Performance impact is minimal
- Integration points are validated
- Documentation is complete and clear
- Testing procedures are provided

**Security Validation Checklist:**

- Input validation prevents injection attacks
- File access stays within project boundaries
- Command execution is safely sandboxed
- Permission checks are comprehensive
- Error messages don't leak sensitive information

**Final Output Requirements:**

1. **Configuration Summary**: Clear description of what hooks were created
2. **File Locations**: Absolute paths to all created/modified files
3. **Testing Instructions**: How to validate hooks work correctly
4. **Usage Examples**: Demonstrate hooks in action
5. **Troubleshooting**: Common issues and debugging steps
6. **Integration Notes**: How hooks work with existing commands/agents

Present final hook configuration location and confirm successful generation with comprehensive testing guidance.
