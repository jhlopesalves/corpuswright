# AGENTS.md

Instructions for coding agents working on the CorpusWright repository. Read this before making changes.

## Validation

After making changes, and before committing, run these three commands from the repository root. All three must pass.

```bash
# Rust core library tests
cargo test --manifest-path crates/corpuswright-core/Cargo.toml

# Tauri backend check
cargo check --manifest-path apps/desktop/src-tauri/Cargo.toml

# Frontend build
npm --prefix apps/desktop run build
```

These run identically on Windows, macOS, and Linux. Don't wrap them in `powershell` or `cmd.exe` invocations — agents often run in a Linux sandbox, and shell-specific commands will fail there.

## Testing policy

These are hard constraints. They exist to keep private and copyrighted material out of the repository.

- Test fixtures in `crates/corpuswright-core/tests/fixtures/` must stay tiny, deterministic, and entirely synthetic. Never add real research data, copyrighted material, or large files.
- The public demo corpus in `examples/corpora/public-domain-demo/` must contain only synthetic or verifiable public-domain text.
- Never commit anything to `.local-corpora/`, `local-corpora/`, `manual-corpora/`, `sample-corpora-local/`, or `coragrarian/`. These are gitignored and reserved for local private testing.

## Writing documentation

Write every document as a plain description of the software's current, permanent behaviour, for a reader who knows nothing about how the code came to be. If a sentence sounds like a status report, a changelog entry, or a note to yourself, rewrite it as a description.

That principle covers most cases. Concretely, it rules out:

- **Development-process references.** No "in this pass", "new in this version", "recently changed", or "has been removed for v1". State current behaviour as fact, not as a diff from some earlier state.
- **Explanatory scaffolding.** No "Problem: … Solution: we use …" structure, no parenthetical justifications in headings such as "(Why X Fails)" or "(Honesty)". Make the claim directly.
- **Maths notation in prose.** Write `at least 0.70` and `the top 3 lines`, not `$\ge 0.70$` or `$N = 3$`.
- **Mechanically symmetrical lists.** Vary sentence and bullet length. A list where every item is the same shape and length reads as generated.

Two conventions that aren't about voice:

- Use British spelling — "artefact", "normalise", "behaviour" — in prose. Code identifiers, filenames, and API names stay exactly as written, even when that means American spelling.
- The legacy PySide prototype documentation lives in `docs/archive/`. Don't present archived content as describing the current application.

## Repository structure

```
crates/corpuswright-core/   Rust library: extraction, cleaning, search, export, repeated artefacts
apps/desktop/               Tauri v2 desktop app with TypeScript/Vite frontend
legacy/pyside/              original PySide6 implementation, kept for reference
docs/                       design notes and reference documentation
docs/archive/               archived documentation from the legacy PySide prototype
examples/                   example corpora and usage material
```
