# Bugbot Review Guidelines

This repo is a TypeScript Stagehand + Browserbase deep research agent. Review changes as production research-pipeline code, not just a demo script.

## High-Priority Review Areas

- Verify Browserbase Search API, Fetch API, and Stagehand API usage against the installed SDK types and runtime behavior.
- Check that benchmark inputs are preserved and actually affect the run, especially `init_url`, `precomputed_rubric`, task IDs, and category metadata.
- Treat fetched and rendered web page content as untrusted evidence. Flag any path where page text can become instructions for planning, synthesis, verification, or strategy updates.
- Check retrieval metadata integrity: requested URL vs final URL, timestamps, content hashes, excerpt hashes, source IDs, and rejected-source diagnostics should not contradict accepted evidence.
- Review verification logic conservatively. Key findings and claim-map entries should only pass when their cited source IDs exist and the cited text supports the claim.
- Watch for cost and reliability regressions: unnecessary browser sessions, unbounded parallel fetches, missing early exits, repeated failed URLs, and leaked Stagehand sessions.
- Confirm generated artifacts, benchmark output, workspaces, `.env`, API keys, and live credentials are never committed or logged.

## Project Conventions

- Keep changes scoped; this is intentionally a single-file template plus docs.
- Prefer deterministic fallbacks when model or browser steps fail.
- Preserve auditability in Markdown and JSON outputs.
- Avoid broad refactors unless they directly reduce a real bug risk.
