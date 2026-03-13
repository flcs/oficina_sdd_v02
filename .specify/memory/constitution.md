<!-- 
SYNC IMPACT REPORT - Constitution v1.0.0
=========================================
- Version Change: Template → 1.0.0 (MAJOR - initial governance framework)
- Ratification Date: 2026-03-13
- Modified Principles:
  ✓ Principle 1: Test-Driven Development (NEW - core discipline)
  ✓ Principle 2: Object-Oriented Programming Paradigm (NEW - architectural core)
  ✓ Principle 3: SOLID Principles (NEW - design non-negotiable)
  ✓ Principle 4: Object Calisthenics (NEW - code discipline)
  ✓ Principle 5: Strict TypeScript Typing (NEW - type safety mandate)
- Dependencies:
  ✓ plan-template.md - Constitution Check section aligns with 5 core principles
  ✓ spec-template.md - User stories align with SOLID and OOP requirements
  ✓ tasks-template.md - Task organization can reflect principle-driven development
- Follow-up items: None deferred; all placeholders resolved
- Template Status: .specify/templates/constitution-template.md remains unchanged for reference
-->

# oficina_sdd_v02 Constitution

## Core Principles

### I. Test-Driven Development (NON-NEGOTIABLE)
All code MUST be written following Test-Driven Development (TDD) principles. Tests are written
before implementation. The Red-Green-Refactor cycle is strictly enforced: write failing tests,
implement minimal code to pass tests, then refactor for clarity and maintainability. No code
enters the codebase without comprehensive test coverage. Integration tests MUST verify contracts
between components and service interactions.

### II. Strict Object-Oriented Programming Paradigm
All code MUST adhere to Object-Oriented Programming principles. Design around classes, objects,
and their interactions. Encapsulation is mandatory—data and behavior must be properly bundled
within classes with appropriate access modifiers. Inheritance and polymorphism MUST be used
appropriately. Pure functional approaches are acceptable ONLY as supporting utilities, never
as primary architecture. Every module MUST be organized as a cohesive object-oriented domain.

### III. SOLID Principles (Non-Optional)
All classes and modules MUST comply with SOLID principles:
- **S**ingle Responsibility: One reason to change per class
- **O**pen/Closed: Open for extension, closed for modification
- **L**iskov Substitution: Subtypes must be substitutable for their base types
- **I**nterface Segregation: Clients depend on focused, small interfaces
- **D**ependency Inversion: Depend on abstractions, not concrete implementations

Violations MUST be documented and justified with explicit architectural rationale.

### IV. Object Calisthenics Discipline
Code MUST follow Object Calisthenics constraints:
- One level of indentation per method maximum
- Do not use the `else` keyword; use early returns or polymorphism
- Wrap all primitives and strings in value objects
- Collections allowed only at the organizational boundary; never mixed with business logic
- One dot per line—no chained method calls
- Do not abbreviate variable or method names
- Keep all entities small (classes under 50 lines, methods under 10 lines)
- No more than two instance variables per class
- No getters/setters; use proper objects and messaging patterns
- All classes MUST have a single, testable responsibility

### V. Strict TypeScript Typing
Full, strict TypeScript typing is MANDATORY across all code:
- `strict: true` MUST be enabled in tsconfig.json
- ALL variables, function parameters, and return types MUST have explicit type annotations
- `any` type is FORBIDDEN except in isolated, documented exceptions
- Null/undefined handling MUST be explicit using `| null` or `| undefined` or `?:` patterns
- Generic types MUST be fully specified—no naked generics
- Type guards and narrowing MUST be employed for runtime safety
- All external library types MUST be explicitly imported and used

## Technical Requirements

All code MUST be written in **TypeScript** with strict type checking enabled.

### Build & Runtime Environment
- Minimum Node.js version: 18.0.0
- Package manager: npm with lockfile (package-lock.json)
- Transpilation: TypeScript compiler (tsc) with strict configuration
- No JavaScript files in src/; all source code MUST be TypeScript

### Code Organization
- Source code resides in `src/` directory
- Tests co-located with source or in `tests/` directory with identical structure
- Clear separation between domain logic, application services, and infrastructure
- Each bounded context MUST be isolated within its own module

## Development Workflow

### Testing Requirements
- Unit tests for all business logic and algorithms
- Integration tests for component interactions and service boundaries
- Acceptance tests for user-facing features
- Minimum 80% code coverage; exceptions MUST be explicitly documented
- Test naming MUST clearly describe behavior being tested
- Use Given-When-Then structure for test descriptions

### Code Review Standards
Every commit MUST pass automated checks:
- TypeScript compilation with strict mode enabled
- All tests passing (unit, integration, and acceptance)
- Linting checks (ESLint or equivalent) passing
- Code coverage thresholds met
- SOLID principle adherence verified
- Object Calisthenics compliance checked

### Clarity and Maintainability Priorities
- Method names MUST clearly express intent and return expectations
- Class names MUST represent single, cohesive responsibilities
- Comments MUST explain "why", never "what" (code should be self-documenting)
- Avoid clever or compact code; favor readability and explicitness
- Variable names MUST be full words, never abbreviated
- Complex logic MUST be broken into smaller, named methods

## Governance

This Constitution supersedes all other coding guidelines and practices in this project.
All pull requests MUST explicitly verify compliance with each of these five core principles
before approval. Violations require explicit justification and architectural review by at
least one other team member. The constitution MUST be reviewed quarterly for relevance and
may be amended through documented consensus with technical leadership.

Amendments to this constitution require:
1. Clear documentation of the change rationale
2. Migration plan for existing code (if applicable)
3. Approval from project stakeholders
4. Update to CONSTITUTION_VERSION following semantic versioning

For runtime development guidance and tool configuration, refer to the project's development
documentation in `docs/`.

**Version**: 1.0.0 | **Ratified**: 2026-03-13 | **Last Amended**: 2026-03-13
