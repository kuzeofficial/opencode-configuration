# OpenCode Configuration

Configuration with custom coding rules, MCP servers, and plugins optimized for maintainability and readability.

---

## Configuration

### Custom Coding Rules

Coding rules prioritize maintainability and readability:

- Readability 10x more important than cleverness
- Simple is better than complex
- Functionality over brevity
- Explicit over implicit

### Core Principles

- Flexible file sizing (no arbitrary limits)
- Logical grouping of related code
- Shallow nesting for readability
- Descriptive names (3+ character minimum)
- Common abbreviations only (id, db, api)
- Verb-based booleans (isActive, hasPermission)
- UPPER_SNAKE_CASE constants
- Shorter ternary when clearer
- Explicit null checks
- Minimal type inference
- Extract after 2-3 occurrences
- Self-documenting code
- Happy path + edge cases
- Formatter-agnostic
- Dependency injection pattern
- Readability first, optimize later
- Idiomatic code patterns

---

## MCP Servers

### Active (6)

1. **context7** - Documentation search
   - Search documentation using natural language
   - Optional: CONTEXT7_API_KEY

2. **gh_grep** - GitHub code search
   - Find real-world code examples
   - Useful for learning patterns

3. **memory** - Persistent memory
   - Store information across sessions
   - Simple key-value storage

4. **sequential_thinking** - Complex reasoning
   - Step-by-step problem solving
   - Useful for multi-step tasks

5. **sentry** - Error tracking (optional)
   - Monitor and debug errors
   - OAuth authentication

6. **figma** - Figma integration
   - Access and modify Figma designs
   - Requires: FIGMA_PERSONAL_ACCESS_TOKEN

---

## Plugins

### Active (2)

1. **opencode-supermemory**
   - AI-powered semantic memory
   - Better organization and search capabilities

2. **oh-my-opencode**
   - Background agents
   - Pre-built LSP/AST/MCP tools
   - Curated agents for common tasks

---

## Commands

### Custom (4)

- /test - Run tests with coverage
- /lint - Run linting and fix
- /typecheck - TypeScript type check
- /build - Build project

---

## System

- Default Agent: build
- Theme: opencode
- Autoupdate: enabled
- Compaction: auto + prune enabled

---

## File Structure

```
.config/opencode/
├── opencode.jsonc           # Main configuration
├── OPENCODE_RULES.md        # Coding rules
├── .env.example              # Environment template
├── package.json              # Plugin dependencies
├── .gitignore               # Git patterns
└── skill/                   # 31 skills
```

---

## Rules File

Path: ~/.config/opencode/OPENCODE_RULES.md

OpenCode automatically reads and applies these rules when generating code.

---

## Quick Start

```bash
# Initialize
opencode

# Check MCP status
opencode mcp list
```

---

## Support

- Docs: https://opencode.ai/docs
- Discord: https://opencode.ai/discord
- GitHub: https://github.com/anomalyco/opencode

---