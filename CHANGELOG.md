# Changelog

All notable changes to this project will be documented in this file.

## [0.1.4] - 2026-04-01

### Added
- Migrated the documentation engine from Sphinx/ReadTheDocs to **MkDocs** with the **Material for MkDocs** theme.
- Implemented a custom documentation "Clinical Architect" design system with optimized dark/light modes and Inter/JetBrains Mono typography.
- Integrated **Plausible Analytics** for documenting telemetry (hash, outbound links, and tagged events).
- Added a dynamic **PyPI Downloads badge** to the global documentation navbar.

### Changed
- Transitioned the official project domain to **vibeblocks.org**.
- Updated `project.urls` in `pyproject.toml` to reflect the new domain and structured documentation index.

## [0.1.3] - 2026-03-11

### Added
- `exception_sanitizer` callback field on `ExecutionContext` and `format_exception()` helper method, enabling custom sanitization of exception messages before they are written to the execution trace.
- Named error hierarchy: `VibeBlocksError` (base), `BlockExecutionError`, `BlockTimeoutError` (timeout-specific), and `ChainExecutionError` — allowing callers to catch failures at any granularity.
- `RetryPolicy` now enforces hard safety limits via `__post_init__`: `max_attempts` is capped at `MAX_ATTEMPTS_LIMIT` (100) and `max_delay` is capped at `MAX_DELAY_LIMIT` (3600 s). Negative values for `max_attempts`, `delay`, and `max_delay` are automatically clamped to zero.
- `is_async_callable()` utility (in `vibeblocks.utils.inspection`) now correctly detects async callables wrapped in `functools.partial` and class instances with an `async def __call__` method.
- Shared `_TASK_TIMEOUT_EXECUTOR` (`ThreadPoolExecutor`) for synchronous block timeouts, reducing thread-creation overhead when many timed blocks run concurrently in the same process.

### Changed
- `ExecutionContext.from_json()` now raises `ValueError` with descriptive messages for malformed input (invalid top-level structure, trace format, metadata type, or `completed_blocks` type), replacing silent failures with explicit errors.

## [0.1.2] - 2026-03-04

### Added
- Added a structured documentation navigation index for the VibeBlocks docs site.
- Included the root `CHANGELOG.md` in the published documentation pages.

### Changed
- Renamed the `Flow` parameter `steps` to `blocks`, and updated docs and examples to match the new API naming.

## [0.1.1] - 2026-02-28

### Changed
- Updated the package metadata `Documentation` URL to point to the live docs site at `https://vibeblocks.aadigitalbusiness.com`.
- Added Wrangler configuration for deploying the Sphinx documentation to Cloudflare Workers assets.

## [0.1.0] - 2026-02-28

### Added
- Initial public deployment of VibeBlocks.
- Core components: `Block`, `Chain`, `Flow`, `ExecutionContext`.
- Resilience policies: `RetryPolicy`, `FailureStrategy`.
- Runtime runners: `SyncRunner`, `AsyncRunner`.
- Dynamic execution support through `VibeBlocks.run_from_json`.
- Documentation and initial project structure.
- `py.typed` marker for type checking support.
