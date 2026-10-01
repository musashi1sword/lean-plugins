# Testing guide (read when writing tests)

Adapted from JavaScript Mastery's `test` skill (MIT licence).

## Rules

- **Never change application code to make a test pass**, and never weaken an assertion. A test that fails because the code is wrong has done its job: report it as a bug.
- **Extend existing test files; don't duplicate them.** If a test file already covers the source file, add cases to it. If existing tests look wrong, flag them; don't silently rewrite them.
- **Config files:** create a minimal one only if the runner can't run without it. Never edit an existing config.
- **Security-sensitive code** (auth, login, sessions, tokens, permissions, roles, payments, webhooks, checkout, personal data): always add cases for unauthorised or forbidden access, missing, expired or tampered credentials, and secrets or sensitive fields not leaking into responses or logs.

## What to write, by file type

| Type | Write |
|---|---|
| Logic | Unit tests with real inputs and outputs; cover edge and error cases thoroughly; mock only true boundaries (network, filesystem, clock, randomness) |
| Component | Render it, interact as a user would, and assert what the user sees (text, roles, disabled or expanded state). Never assert internal state or class names. |
| Page or flow | With an end-to-end tool: the main path plus one failure path. Otherwise test it at component level. |
| API or server | Call the route with representative requests; assert status, response shape and error responses (bad input, unauthorised, not found). Mock the database or external services at the boundary only. |
| CLI | Run it with arguments; assert output, exit code and side effects; include one invalid-arguments case |

## Coverage order

1. Happy path
2. Edge cases: empty, null, zero, boundaries, max length, unicode
3. Errors: invalid input, a dependency failing, network error, unauthorised, not found
4. State changes: initial state → action → expected new state
5. Accessibility (UI): reachable by keyboard, accessible names, labels tied to inputs

## Craft

- Name tests as sentences: "returns null when the cart is empty".
- Test one concept per test, and lay each out as Arrange → Act → Assert.
- Test the public interface, not internals. Don't mock what you own.
- Keep tests deterministic: freeze the clock, use no real network, don't depend on test order. Await every async call.
- Selectors: prefer role, then label, then text; use test IDs as a last resort. For end-to-end tests, wait on assertions, never on fixed timeouts.

## Running

Use the quiet reporter (`--reporter=dot`, `-q`). On a retry, rerun only the failing file.
- Test is wrong → fix the test.
- Code is wrong → leave the test failing and report it as a bug.

Stop when everything passes or only real bugs remain.

Report: the tests written (file, count, what they cover), the run result, bugs found, and anything not covered with the reason.
