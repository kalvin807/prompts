# General Rules

## Direction
- Prefer pure functions and dependency injection. Isolate side effects.
- Fail loud. Prefer `throw` without `catch`. Only catch when transforming the error or strictly recovering. Never silence errors.
- When acting as an AI agent, verify your own logic line-by-line. Aggressively prune redundant comments and tests that "mock the mock."

## Code Style
- Flatten code with early returns (`continue`, `return`, `break`) to avoid deep `if/else` nesting.
- Prefix functions with `maybe_` if they can return `None`/`null`/`undefined` (e.g., `maybe_get_user`).
- Docstrings explain *why* or *how* — non-trivial info only. Do NOT write one-liners that repeat the function name.
- Place imports at the top-level of the module. Never import inside functions.
- Use implicit boolean checks (`if obj:`) generally. Explicitly check `0` or empty strings only when they are valid values. Avoid double negation.

## Plan Style
- Verify you have the service layer context before writing code. Do not guess database schemas.
- Clearly define what is in scope vs. out of scope.
- PR descriptions and summaries include the "Why", the "Scope", and any agentic limitations (e.g., "Tests need human verification").

## Test Style
- Use standalone functions, not classes. Keep tests short, focused, and flat.
- Avoid mocking whenever possible. Prefer testing against real helpers, pure logic, or lightweight fakes.
  - When mocking is unavoidable (e.g., 3rd-party APIs), use `mocker.patch.object` (Python) or `vi.spyOn` (JS). Do NOT mock internal implementation details.
- Heavily prefer table-driven tests (`pytest.mark.parametrize`, `test.each`) to deduplicate logic and cover edge cases.
- Share fixtures for data setup. Do not duplicate setup logic across tests.
- Design pure functions first for testability. Test the output, not the internal state.

---

# Python

- Use PEP 604 union types exclusively (`X | Y`). Do NOT use `Union[X, Y]` or `Optional[X]`.
- Use `pytest`-style fixtures and parameterization.
- Create reusable fixtures for data/mocks. Do not repeat setup.

---

# TypeScript / JavaScript

- Strict TypeScript. Avoid `any` unless absolutely unavoidable.
- Keep `useEffect` simple. Read "You might not need an effect" guidelines.
- Invalidate React Query caches after mutations.
- Surface Zod errors to the user on the frontend (UX only). Rely on Pydantic on the backend for security/integrity.
- Use `visibility` or `opacity` for hiding components with animations — avoid breaking layout.
- Test scrolling behavior on long content.
- Ensure dark mode compatibility. Do NOT hardcode hex black/white on text.
