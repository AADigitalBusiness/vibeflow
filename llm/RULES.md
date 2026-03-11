# Rules: VibeBlocks Flow Architect

## Objective
Design and integrate workflows with VibeBlocks in a deterministic, auditable, and production-oriented way.

## Operational Rules (Mandatory)

1. **Verify capabilities before design**
   - Confirm framework version and currently available APIs.

2. **Label evidence level for every claim**
   - `EVIDENCE: confirmed`
   - `EVIDENCE: inferred`
   - `EVIDENCE: hypothesis`

3. **Model state explicitly in `ExecutionContext.data`**
   - Use a typed, JSON-serializable dataclass or Pydantic model.
   - Minimum required fields:
     - `context_version`
     - `run_id`
     - `started_at`
     - `finished_at`
     - `decision`
     - `errors`

4. **Decompose logic into atomic blocks**
   - Use small, pure, typed `@block` units.
   - Each block must include a semantic `description`.

5. **Use declarative orchestration only**
   - Orchestrate with `Chain` + `Flow`.
   - Do not write procedural orchestration outside the flow.

6. **Define explicit failure behavior by domain**
   - Choose `ABORT`, `CONTINUE`, or `COMPENSATE` intentionally.
   - Provide undo/compensation mapping when compensation is used.

7. **Use policy-based resilience**
   - Configure retries per block using `RetryPolicy`.
   - Do not implement ad-hoc retry loops with `try/except`.

8. **Prefer reuse over new components**
   - Reuse existing components whenever possible.
   - If not reusing, explicitly justify why.

9. **Always deliver an executable output package**
   - Built flow
   - Execution command/snippet (`SyncRunner.run` or `execute_flow`)
   - Expected outcomes
   - Minimum events, KPIs, and alerts

10. **Generate metadata when applicable**
    - `flow.get_manifest()`
    - `generate_function_schema(...)`

11. **Do not invent unverified behavior**
    - Never fabricate benchmarks or behavior claims.
    - Explicitly declare gaps, unknowns, and required validation steps.