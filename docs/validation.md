# Validation

Checked locally on 2026-09-11 against Pi 0.84.4 declarations.

## Commands and outcomes

- `git init`: created local repository; no remote, commit, push, or staging.
- `npm install --ignore-scripts`: the machine's npm shim initially used aube. Replaced its generated lock with a portable npm `package-lock.json` using the installed real npm CLI. No absolute/local cache paths remain in that lockfile.
- `npm run check`: typecheck and 10 Node tests pass with the real Node/npm installation on PATH.
- `node node_modules/typescript/bin/tsc --noEmit`: passes independently.
- `node --test test/*.test.ts`: all 10 tests pass independently.
- README audit: all checks pass. Its first pass rejected `npm ci` as an unrecognized setup example; README now uses the equally valid `npm install --ignore-scripts`.
- `git diff --cached --quiet`: passes (nothing staged).

One later invocation through the machine's aube npm shim failed while trying to auto-install because a transitive registry response lacked `dist.integrity`. The implementation typecheck/tests pass using the actual installed Node executable directly. This is an environment/package-manager limitation, not a suppressed test failure. No integrity verification was disabled.

## Tested behavior

- Exact Astra/Sol/Luna model selection on both supported providers, and non-target no-op behavior.
- Family versus Astra instruction isolation, including switching between them.
- Every applicable rule independently disabled while all other rules remain unchanged.
- Active-tool gates for collaboration and planning, including disabled tools.
- No invented Codex tool names in prompts for a tool-less session.
- Strict config schema, malformed JSON, unknown IDs/keys, unreadable paths, missing file defaults, and live config edits between user turns.
- Base prompt preservation, deterministic output, repeated calls without accumulation, and exact previous-suffix removal on model switching.
- Real extension factory/hook wiring with a minimal in-memory Pi host and temporary home (no live Pi settings touched).
- Every rule file referenced exactly once, substantive text, source/test line ceiling.
- Rules documented as verbatim are whitespace-normalized excerpts of the bundled official source snapshots.

## Complexity evidence

`wc -l src/*.ts test/*.ts` reports 313 lines, including blanks, catalog metadata, and tests:

| File | Lines |
|---|---:|
| src/catalog.ts | 72 |
| src/guidance.ts | 76 |
| src/index.ts | 21 |
| test/guidance.test.ts | 144 |

Package/TypeScript JSON configuration contains only declarative settings and three short script commands; including all those files still leaves the total far below 1,000. There are no other executable files, generators, or hidden fixture code. Source snapshots include documentary OpenAI example programs but are not loaded as code. Only `rules/*.md` is injected, as text.

## Not verified

No live model requests, TUI smoke session, credentials access, billing changes, installation into the user's Pi settings, or behavioral model evals were performed. Source-based prompting improvements are not proof of model-quality gains. Later Pi extensions can still change the prompt. Provider phase replay and Pi compaction correctness are outside this extension's tests. Compatibility with Pi versions newer than 0.84.4 is not claimed.
