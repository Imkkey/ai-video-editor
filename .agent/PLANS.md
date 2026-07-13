# Execution Plans

An ExecPlan is a self-contained implementation plan for a complex feature.

Use an ExecPlan when a task:

- changes more than one major subsystem;
- introduces a new external integration;
- adds a database migration;
- creates a long-running media pipeline;
- changes a public API contract;
- is expected to require several implementation and validation steps.

Store plans in:

docs/plans/<milestone>-<short-name>.md

Every ExecPlan must contain the following sections.

## Purpose

Describe the user-visible outcome in plain language.

## Current state

Describe relevant existing behavior, files, APIs, models, and limitations.

## Scope

List exactly what is included.

## Non-goals

List what must not be implemented in this plan.

## Assumptions

Record decisions made without asking the user.

## Proposed design

Describe components, boundaries, data flow, and important interfaces.

## Data model changes

List tables, columns, indexes, constraints, and migrations.

## API changes

List endpoints, request schemas, response schemas, and errors.

## Frontend changes

List routes, screens, components, and state transitions.

## Implementation sequence

Use small numbered steps. Each step must leave the repository in a coherent
state where possible.

## Validation

List exact commands and manual checks.

## Failure and recovery

Explain retries, idempotency, cleanup, rollback, and partial-failure behavior.

## Security considerations

Describe input validation, path safety, secret handling, and command execution.

## Progress

Maintain a checklist:

- [ ] Planned
- [ ] Implemented
- [ ] Tests added
- [ ] Validation passed
- [ ] Documentation updated

## Decision log

Record important decisions with a date and short rationale.

## Discoveries

Record unexpected repository facts or constraints discovered during work.

## Outcome

After implementation, describe what actually shipped, what changed from the
plan, and what remains.
