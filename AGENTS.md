
# Project mission

Build a local-first AI-assisted video rough-cut editor.

The application takes narration audio or video, transcribes it, divides the
speech into semantic beats, matches beats with user-provided visual assets,
lets the user review selections, and renders an editable rough cut.

This is not a full nonlinear video editor. Keep the product focused on
semantic planning and rough-cut generation.

# Sources of truth

Before making architectural or product changes, read:

- docs/PRODUCT_SPEC.md
- docs/ARCHITECTURE.md
- docs/DATA_MODEL.md
- docs/API_CONTRACT.md
- docs/MILESTONES.md
- docs/STATUS.md
- docs/REFERENCE_EDITING_WORKFLOW.md
- .agent/PLANS.md

If documents disagree, use this priority:

1. Current user task
2. AGENTS.md
3. docs/PRODUCT_SPEC.md
4. docs/ARCHITECTURE.md
5. docs/MILESTONES.md
6. Reference workflow

# Execution rules

- Implement only the milestone explicitly requested by the user.
- Do not silently implement future milestones.
- Keep diffs scoped to the requested behavior.
- Do not rewrite working modules without a concrete reason.
- Do not change public API contracts without updating API_CONTRACT.md.
- Do not introduce a production dependency without explaining why it is needed.
- Do not commit changes unless explicitly requested.
- Record important architectural decisions in docs/DECISIONS.md.
- Update docs/STATUS.md after every completed milestone.
- For work touching multiple subsystems, create or update an ExecPlan under
  docs/plans/ before implementation.
- Prefer simple, replaceable provider interfaces over direct vendor coupling.
- Make routine implementation assumptions instead of blocking on minor questions.
  Record those assumptions in the plan or decision log.

# Architecture constraints

- Backend: Python and FastAPI.
- Frontend: React and TypeScript.
- Persistence: SQLAlchemy with SQLite for the MVP.
- Database schema changes must use Alembic migrations.
- Media processing must use FFmpeg and FFprobe.
- Long media operations must run through the job system, not inside an HTTP request.
- AI integrations must be behind typed provider interfaces.
- Tests must use deterministic mock providers and must not require paid API calls.
- Model identifiers must come from environment variables.
- Store timestamps internally as integer milliseconds.
- Store filesystem paths relative to the configured application data root.
- Use UUIDs for externally visible entity IDs.
- Use UTC for stored timestamps.
- Preserve media aspect ratios by default.
- The default render canvas is 1920x1080 with a black background.
- The MVP primarily uses hard cuts.

# Security rules

- Never expose API keys to frontend code.
- Never commit secrets or real credentials.
- Provide .env.example without secret values.
- Never log authentication headers, API keys, or complete sensitive payloads.
- Do not use shell=True for media subprocesses.
- Pass FFmpeg arguments as an explicit argument list.
- Validate uploaded file type, extension, size, path, and storage destination.
- Prevent path traversal.
- Do not implement internet scraping.
- Treat all uploaded filenames and metadata as untrusted input.

# Code quality

Backend:

- Use type annotations.
- Validate external input with Pydantic.
- Separate API routes, services, repositories, provider adapters, and domain models.
- Keep media command construction isolated and unit-tested.
- Use structured application errors.
- Add unit tests for domain logic and integration tests for API behavior.

Frontend:

- Enable strict TypeScript.
- Keep API calls in a typed client layer.
- Represent loading, empty, error, and success states.
- Avoid duplicating backend domain rules in components.
- Use accessible controls and keyboard navigation where practical.
- Add component tests for important workflows.

# Validation

Before declaring a milestone complete:

1. Run backend formatting and lint checks.
2. Run backend type checks.
3. Run backend tests.
4. Run frontend lint.
5. Run frontend type checks.
6. Run frontend tests.
7. Run the production frontend build.
8. Run the smallest relevant end-to-end or smoke test.
9. Review the complete diff for unrelated changes.
10. Update documentation and status.

If a command cannot run, report the exact command, error, and reason.

# Definition of done

A task is complete only when:

- requested behavior is implemented;
- tests cover the important success and failure paths;
- relevant checks pass;
- public contracts are documented;
- setup instructions remain accurate;
- no placeholder implementation is presented as complete;
- docs/STATUS.md reflects the actual repository state.

# Final task report

At the end of every task report:

- summary of implemented behavior;
- files changed;
- migrations added;
- commands run and their results;
- manual verification steps;
- assumptions made;
- remaining risks or limitations;
- suggested commit message.
