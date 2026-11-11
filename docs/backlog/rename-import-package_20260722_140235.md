# Rename import package `opendata-b3` → `opendata_b3`

Issue: #109 — blocks #3 and the whole epic #2 (B3 ingestion dehydration).

The scaffold substituted the hyphenated **distribution** name into the **import** package, so
`src/opendata-b3/` + every `from opendata-b3… import` was a parse-time `SyntaxError` and the whole
`_internal` tree was unimportable.

## Checklist

- [x] `git mv src/opendata-b3 src/opendata_b3`
- [x] Rewrite the 52 dotted imports `opendata-b3.` → `opendata_b3.` in `src/` and `tests/`
- [x] `pyproject.toml`: `packages = [{ include = "opendata_b3", from = "src" }]`
- [x] Keep the hyphenated `opendata-b3` as the distribution name (`name`, URLs, keywords,
      `version("opendata-b3")`, CI `PACKAGE_NAME`)
- [x] Decorate placeholder `main()` with `@type_checker` (typing gate, surfaced by the rename)
- [x] Verify: `compileall` clean, `import opendata_b3` + deep submodule import OK, 43 tests pass
- [x] Capture the BlueprintX scaffold lesson (store + index + git-ignored repo mirror)
- [x] Merge PR and run `/release-py` — merged as `b4fd95e` (#110), released **v0.1.0**

**Completed — kept as a record.** Every item is done; this ledger stays as the reviewable
account of the rename. Follow-on work continues in `slim-ingestion-base_20260722_173356.md`
(issue #3), which the rename unblocked.
