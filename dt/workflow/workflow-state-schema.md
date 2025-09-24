# Workflow State JSON Schema

## Purpose
Defines the structure for workflow-state.json files used by enterprise workflow commands to maintain project state, discovered tools, and implementation progress.

## Schema Structure

### Core Schema
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "required": ["metadata", "project_metadata"],
  "properties": {
    "metadata": {
      "type": "object",
      "required": ["version", "created_at", "last_updated"],
      "properties": {
        "version": {"type": "string", "pattern": "^\\d+\\.\\d+\\.\\d+$"},
        "created_at": {"type": "string", "format": "date-time"},
        "last_updated": {"type": "string", "format": "date-time"},
        "workflow_chain_position": {"type": "integer", "minimum": 1, "maximum": 7}
      }
    },
    "project_metadata": {
      "type": "object",
      "required": ["discovered_tools"],
      "properties": {
        "discovered_tools": {"$ref": "#/$defs/discovered_tools"}
      }
    }
  },
  "$defs": {
    "discovered_tools": {
      "type": "object",
      "required": ["ecosystem", "discovery_status"],
      "properties": {
        "ecosystem": {
          "type": "string",
          "enum": ["nodejs", "rust", "python", "go", "java", "ruby", "php", "dotnet", "make", "mixed", "unknown"]
        },
        "discovery_status": {
          "type": "string",
          "enum": ["complete", "partial", "failed", "not_started"]
        },
        "package_manager": {"$ref": "#/$defs/package_manager"},
        "build_system": {"$ref": "#/$defs/build_system"},
        "quality_tools": {"$ref": "#/$defs/quality_tools"},
        "testing": {"$ref": "#/$defs/testing"},
        "validation_sequence": {
          "type": "array",
          "items": {"type": "string"},
          "description": "Ordered list of command references for quality gate validation"
        }
      }
    },
    "package_manager": {
      "type": "object",
      "properties": {
        "name": {"type": "string"},
        "version": {"type": "string"},
        "install_cmd": {"type": "string"},
        "install_dev_cmd": {"type": "string"},
        "update_cmd": {"type": "string"},
        "verified": {"type": "boolean", "default": false}
      }
    },
    "build_system": {
      "type": "object",
      "properties": {
        "compile_cmd": {"type": "string"},
        "build_cmd": {"type": "string"},
        "type_check_cmd": {"type": "string"},
        "clean_cmd": {"type": "string"},
        "watch_cmd": {"type": "string"},
        "verified": {"type": "boolean", "default": false}
      }
    },
    "quality_tools": {
      "type": "object",
      "properties": {
        "lint_cmd": {"type": "string"},
        "lint_fix_cmd": {"type": "string"},
        "format_cmd": {"type": "string"},
        "format_check_cmd": {"type": "string"},
        "security_check_cmd": {"type": "string"},
        "verified": {"type": "boolean", "default": false}
      }
    },
    "testing": {
      "type": "object",
      "properties": {
        "test_cmd": {"type": "string"},
        "test_watch_cmd": {"type": "string"},
        "test_coverage_cmd": {"type": "string"},
        "test_unit_cmd": {"type": "string"},
        "test_integration_cmd": {"type": "string"},
        "test_e2e_cmd": {"type": "string"},
        "verified": {"type": "boolean", "default": false}
      }
    }
  }
}
```

## Example Implementations

### Node.js Project
```json
{
  "metadata": {
    "version": "1.0.0",
    "created_at": "2025-01-15T10:30:00Z",
    "last_updated": "2025-01-15T10:45:00Z",
    "workflow_chain_position": 3
  },
  "project_metadata": {
    "discovered_tools": {
      "ecosystem": "nodejs",
      "discovery_status": "complete",
      "package_manager": {
        "name": "npm",
        "version": "10.2.3",
        "install_cmd": "npm install",
        "install_dev_cmd": "npm install --save-dev",
        "update_cmd": "npm update",
        "verified": true
      },
      "build_system": {
        "build_cmd": "npm run build",
        "type_check_cmd": "npm run type-check",
        "clean_cmd": "npm run clean",
        "watch_cmd": "npm run dev",
        "verified": true
      },
      "quality_tools": {
        "lint_cmd": "npm run lint",
        "lint_fix_cmd": "npm run lint:fix",
        "format_cmd": "npm run format",
        "format_check_cmd": "npm run format:check",
        "verified": true
      },
      "testing": {
        "test_cmd": "npm test",
        "test_watch_cmd": "npm run test:watch",
        "test_coverage_cmd": "npm run test:coverage",
        "verified": true
      },
      "validation_sequence": [
        "package_manager.install_cmd",
        "build_system.type_check_cmd",
        "quality_tools.lint_cmd",
        "testing.test_cmd"
      ]
    }
  }
}
```

### Rust Project
```json
{
  "metadata": {
    "version": "1.0.0",
    "created_at": "2025-01-15T10:30:00Z",
    "last_updated": "2025-01-15T10:45:00Z",
    "workflow_chain_position": 3
  },
  "project_metadata": {
    "discovered_tools": {
      "ecosystem": "rust",
      "discovery_status": "complete",
      "package_manager": {
        "name": "cargo",
        "version": "1.75.0",
        "install_cmd": "cargo fetch",
        "update_cmd": "cargo update",
        "verified": true
      },
      "build_system": {
        "compile_cmd": "cargo build",
        "build_cmd": "cargo build --release",
        "type_check_cmd": "cargo check",
        "clean_cmd": "cargo clean",
        "watch_cmd": "cargo watch -x run",
        "verified": true
      },
      "quality_tools": {
        "lint_cmd": "cargo clippy",
        "format_cmd": "cargo fmt",
        "format_check_cmd": "cargo fmt -- --check",
        "verified": true
      },
      "testing": {
        "test_cmd": "cargo test",
        "test_coverage_cmd": "cargo tarpaulin --out Html",
        "verified": true
      },
      "validation_sequence": [
        "package_manager.install_cmd",
        "build_system.type_check_cmd",
        "quality_tools.lint_cmd",
        "testing.test_cmd"
      ]
    }
  }
}
```

### Python Project
```json
{
  "metadata": {
    "version": "1.0.0",
    "created_at": "2025-01-15T10:30:00Z",
    "last_updated": "2025-01-15T10:45:00Z",
    "workflow_chain_position": 3
  },
  "project_metadata": {
    "discovered_tools": {
      "ecosystem": "python",
      "discovery_status": "complete",
      "package_manager": {
        "name": "pip",
        "version": "23.3.1",
        "install_cmd": "pip install -r requirements.txt",
        "install_dev_cmd": "pip install -r requirements-dev.txt",
        "verified": true
      },
      "build_system": {
        "type_check_cmd": "mypy .",
        "verified": true
      },
      "quality_tools": {
        "lint_cmd": "flake8",
        "format_cmd": "black .",
        "format_check_cmd": "black --check .",
        "verified": true
      },
      "testing": {
        "test_cmd": "pytest",
        "test_coverage_cmd": "pytest --cov=src --cov-report=html",
        "verified": true
      },
      "validation_sequence": [
        "package_manager.install_cmd",
        "build_system.type_check_cmd",
        "quality_tools.lint_cmd",
        "testing.test_cmd"
      ]
    }
  }
}
```

## Usage Guidelines

### For 03-plan-implementation.md
- MUST populate discovered_tools section completely
- MUST verify all discovered commands work
- MUST set discovery_status to "complete" only after validation

### For 04-generate-code.md
- MUST check discovery_status is "complete" before proceeding
- MUST use only discovered commands from validation_sequence
- MUST fail fast if required commands missing

### For other workflow commands
- MAY read discovered_tools for project-specific operations
- SHOULD respect ecosystem-specific patterns
- MUST NOT override or ignore discovered tool configurations

## Validation Rules

1. **Discovery Status Enforcement**: Commands requiring tools MUST check discovery_status is "complete"
2. **Command Verification**: All commands in validation_sequence MUST have verified: true
3. **Ecosystem Consistency**: Discovered commands MUST match declared ecosystem
4. **Required Commands**: validation_sequence MUST contain at least package install command
5. **Command Format**: All command strings MUST be executable shell commands