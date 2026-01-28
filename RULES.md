# OpenCode Coding Rules

You are an AI coding assistant. Follow these rules strictly when writing, modifying, or reviewing code.

---

## CRITICAL RULES

### 1. Readability Over Cleverness

Always prioritize code clarity. Code is read 10x more than written.

- CORRECT: Write explicit, self-documenting code
- INCORRECT: Use clever tricks or overly compact code

### 2. Dependency Injection

Always pass dependencies explicitly as function parameters.

- CORRECT: `function process(database: DB, logger: Logger) {}`
- INCORRECT: `function process() { const db = getGlobalDB(); }`

### 3. No Ternary Operators

Never use ternary operators. Always use if/else statements.

- CORRECT: `if (isActive) { status = 'on'; } else { status = 'off'; }`
- INCORRECT: `status = isActive ? 'on' : 'off';`

### 4. Extract After 2 Repetitions

When code appears 2+ times, immediately extract to a utility function.

- CORRECT: Create `calculateTotal()` after 2nd use
- INCORRECT: Copy-paste similar logic 3+ times

### 5. All Numbers as Constants

Always extract number literals to named constants (except 0 and 1).

- CORRECT: `const MAX_RETRIES = 3; if (attempts > MAX_RETRIES)`
- INCORRECT: `if (attempts > 3)`

### 6. Strict TypeScript Typing

Always use explicit types. No implicit `any`.

- CORRECT: `function process(userId: string): Promise<User>`
- INCORRECT: `function process(userId)`

### 7. Immutable Data

Always create new objects/arrays. Never mutate existing ones.

- CORRECT: `const newArray = [...oldArray, newItem];`
- INCORRECT: `oldArray.push(newItem);`

### 8. No TODOs in Production

Never leave TODO comments. Create GitHub issues instead.

- CORRECT: Create issue, reference in commit
- INCORRECT: `// TODO: Fix this later`

### 9. Early Returns and Guard Clauses

Use early returns and guard clauses to reduce nesting and improve readability. Validate preconditions at the function start and return early.

- CORRECT:
  ```typescript
  function processUser(user: User | null): string {
    if (!user) {
      return 'No user';
    }

    if (!user.isActive) {
      return 'User inactive';
    }

    return processActiveUser(user);
  }
  ```
- INCORRECT:
  ```typescript
  function processUser(user: User | null): string {
    if (user) {
      if (user.isActive) {
        return processActiveUser(user);
      } else {
        return 'User inactive';
      }
    }
    return 'No user';
  }
  ```

---

## NAMING CONVENTIONS

### Variables and Functions

- Minimum 3 characters
- Full words only (no abbreviations except: id, db, api, url, http)
- CORRECT: `userRepository`, `calculateTotalPrice`
- INCORRECT: `usrRepo`, `calcTotPrc`, `x`, `temp`

### Booleans

Always use verb prefixes: `is`, `has`, `can`, `should`

- CORRECT: `isActive`, `hasPermission`, `canExecute`
- INCORRECT: `active`, `permission`, `executable`

### Constants

Always use UPPER_SNAKE_CASE

- CORRECT: `API_BASE_URL`, `MAX_RETRY_COUNT`, `DEFAULT_TIMEOUT`
- INCORRECT: `apiBaseUrl`, `maxRetryCount`

---

## CODE STRUCTURE

### Functions

- No strict length limit - use judgment
- Extract complex logic when nesting exceeds 4 levels

### Files

- Split when exceeding 200-300 lines
- Group related functions together
- One primary concern per file

### Error Handling

Only use try/catch at integration boundaries (API calls, file I/O, external services).

- CORRECT: `try { await fetch(url); } catch (e) { handleError(e); }`
- INCORRECT: Wrap every internal function in try/catch

### Null Checks

Always use explicit checks.

- CORRECT: `if (user === null)` or `if (!user)`
- INCORRECT: `if (user == null)`

---

## TESTING

### Test Location

Place test files adjacent to source files.

- CORRECT: `Button.tsx` + `Button.test.tsx` in same directory
- INCORRECT: Separate `tests/` folder far from source

### Test Coverage

- Test happy path + edge cases
- Include: null, undefined, empty, boundary values
- Name format: `should [behavior] when [condition]`

### Mocking

Only mock external dependencies (APIs, databases, file system).

- CORRECT: Mock `fetch()`, `fs.readFile()`, database calls
- INCORRECT: Mock internal utility functions

---

## DOCUMENTATION

### Comments

Code must be self-documenting. Use comments only for complex algorithms.

- CORRECT: Clear function/variable names that explain purpose
- INCORRECT: `// This function calculates the total` (redundant)

### Forbidden Comment Styles

Never use these patterns:

- "We have X feature here"
- "This is annotated for Y"
- `// TODO: Fix this`

---

## DECISION TREES

### When to Extract Code

```
IF code appears 2+ times
THEN extract to utility function
ELSE keep inline
```

### When to Use Loops vs Functional

```
IF transforming/filtering data
THEN use map(), filter(), reduce()
ELSE IF need break/continue logic
THEN use for/while loop
ELSE choose based on clarity
```

### When to Add Types

```
IF function parameter OR return value
THEN always add explicit type
ELSE IF simple variable assignment
THEN type inference acceptable
```

---

## FORMATTING

Accept project's existing formatter/linter. Do not manually adjust:

- Indentation (2 spaces vs 4 vs tabs)
- Trailing commas
- Line breaks

Maximum line length: 120 characters (flexible)

---

## CHECKLIST

Execute this checklist for every code change:

- No ternary operators (use if/else)
- All dependencies passed as parameters
- No code repetition (2+ times = extract)
- All numbers are named constants (except 0, 1)
- All repeated strings are constants
- Variables/functions: 3+ chars, full words, no abbreviations
- Booleans: is/has/can/should prefix
- Constants: UPPER_SNAKE_CASE
- Types: explicit for all parameters and return values
- Null checks: explicit === null or !variable
- Try/catch: only at integration boundaries
- Data: immutable (no mutations)
- Comments: none unless absolutely necessary
- TODOs: none (create issues instead)
- Tests: adjacent to source, cover happy + edge cases

---

## PRIORITY ORDER

When rules conflict, follow this order:

1. Readability - Choose more readable option
2. Explicit over implicit - Always prefer explicit code
3. Immutability - Never mutate unless performance critical
4. DRY - Extract repetition aggressively
5. Type safety - Explicit types over inference

---

## EXAMPLES

### INCORRECT Example

```typescript
function calc(u) {
  const t = u > 5 ? "high" : "low"; // Ternary + abbrev + magic number
  arr.push(t); // Mutation
  return t;
}
```

### CORRECT Example

```typescript
const THRESHOLD_VALUE = 5;

function calculateUserLevel(userScore: number): string {
  let level: string;

  if (userScore > THRESHOLD_VALUE) {
    level = "high";
  } else {
    level = "low";
  }

  const newArray = [...existingArray, level]; // Immutable

  return level;
}
```

---

## APPLICATION

1. Apply rules automatically during code generation
2. Check against checklist before presenting final code
3. When uncertain, choose the more explicit/readable option
4. When rules conflict, follow priority order