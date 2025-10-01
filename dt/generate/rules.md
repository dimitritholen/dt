---
allowed-tools: Read, Write, Edit, Task, mcp__sequential-thinking__sequentialthinking
argument-hint: [language-or-framework]
description: AI Rules Generator researching industry standard rules for the given tech
---

 Spin up 5-8 parallel sub-agents to search the web for $ARGUMENTS industry standard best practices, coding guidelines, (enterprise) patterns, good habits. 
 Save them as a categorized list to a file called ./rules/$ARGUMENTS.md and make each of the results an actionable rule for AI models to follow during coding. 
  Be as complete as possible when gathering. 
 The goal is to create a comprehensive list, so that if the list is followed, the code quality will be TOP QUALITY and PRODUCTION READY. 
 
**MUST**:
- Use chain of thought with reasoning. 
- Think hard. 
- Only use reputable sources. 
- After each search term as " as of mid 2025"

Be critical of the rules, only add the best rules.
Keep the rules short and compact using good prompt-engineering techniques so they must be followed at all times. 

<example>
# LangGraph 0.6.8 Production Rules

## 1. Architecture & Graph Design

### Graph Structure
- **MUST** choose appropriate agent architecture based on task requirements: ReAct for tool use + multi-step reasoning; multi-agent patterns (Pipeline/Hub-and-Spoke) for complex orchestration.
- **MUST** use subgraphs for modular design in multi-agent systems; communicate with parent graph through overlapping state schema keys.
- **MUST** design nodes as independent, clearly defined units with single responsibilities.
- **NEVER** rely on `recursion_limit` as primary halt mechanism—hitting it indicates design flaws; implement explicit exit conditions based on state.
- **MUST** ensure graphs terminate gracefully through explicit conditional routing, not timeout limits.

### Control Flow
- **MUST** define clear routing logic with explicit conditionals in edges; avoid implicit assumptions about execution order.
- **MUST** use static breakpoints (`interrupt_before`/`interrupt_after`) for predictable HITL patterns; reserve dynamic `interrupt()` for runtime decisions.
- **NEVER** dynamically modify node structure containing multiple `interrupt()` calls—introduces state consistency and resume value errors.

---

## 2. State Management

### State Schema Design
- **MUST** keep state schemas minimal—include only necessary information for graph execution.
- **MUST** define explicit, typed state structures using user-defined schemas (e.g., TypedDict, Pydantic models).
- **NEVER** include extraneous data in state; bloat degrades performance and complicates debugging.

### Reducers (CRITICAL)
- **MUST** define reducer functions for ALL state keys modified by parallel branches—reducers are mandatory, not optional, to prevent `InvalidUpdateError`.
- **MUST** implement fast, optimized reducers—they execute frequently and impact performance.
- **MUST** test reducer logic for commutativity and associativity when operations may occur in any order.

### Persistence
- **MUST** configure checkpointer when compiling graph for production use—enables HITL, error recovery, session memory, time-travel debugging.
- **MUST** use production-grade database adapters (Redis, Postgres, SQLite) for checkpointer backend; avoid in-memory for production.
- **MUST** implement Store interface for cross-thread persistent state (long-term memory); checkpointers alone cannot share data across threads.
- **MUST** use threads to organize conversation sessions; each thread contains sequential checkpoints.

... (REST OF THE RULES OMMITTED)
</example>

<example>
# FastAPI 0.118.0 Production-Ready Coding Rules

## 1. Project Structure & Architecture

### Project Organization

**MUST organize domain logic inside a single root package** (typically `app/` or `src/`), with each feature module containing consistent files: `router.py`, `schemas.py`, `models.py`, `service.py`, `dependencies.py`, and `exceptions.py`.

**MUST use relative imports between modules within the same package** (e.g., `from ..dependencies import get_db`) to maintain portability and avoid coupling to specific deployment structures.

**NEVER mix infrastructure concerns with domain logic** - business logic in service layer must be expressible in plain Python without importing FastAPI or ORM libraries.

### Layered Architecture

**MUST enforce unidirectional dependency flow**: Presentation → Application/Service → Domain → Infrastructure. Inner layers (domain) cannot import from outer layers (routers, dependencies). Use dependency inversion with abstract interfaces at layer boundaries.

**ALWAYS separate Commands (writes) from Queries (reads)** - command operations use rich domain entities and value objects, while query operations can bypass service layer for optimized read-only data transfer objects.

**ALWAYS keep controllers (routers) thin with zero business logic** - routers should only handle HTTP concerns (extracting request data, calling service methods, formatting responses). Move all conditional logic, loops, and calculations to service layer.

### Dependency Injection

**ALWAYS use constructor injection over FastAPI's `Depends()` for core business logic** - reserve `Depends()` exclusively for HTTP layer concerns (authentication, database sessions, request context). Framework-agnostic DI containers enable easier testing and framework migration.

**MUST implement singleton pattern for shared resources using lifespan events** - database connection pools, cache clients, and external service clients should be initialized once during application startup, not per-request.

**ALWAYS chain dependencies to avoid duplication** - FastAPI automatically caches dependency results within a single request scope, so dependencies requiring the same sub-dependency will reuse the computed value.

... (REST OF THE RULES OMMITTED)
</example>