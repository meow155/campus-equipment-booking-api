# AI Log

## Prompt 1

**Prompt:** "Design a Hono API for equipment booking and include overlap validation, error handling, and SQLite-safe queries."

**Result used:** I used the guidance to shape the API contract and business rules, especially the validation logic for start/end times and overlap checks.

**Verification:** I manually checked the implementation against the assignment rubric and ran the live test suite to confirm the behavior.

## Prompt 2

**Prompt:** "Help debug Windows/Node 24 compatibility issues with SQLite dependencies for a local TypeScript app."

**Result used:** I switched to `sql.js`, which works on this environment without a native build toolchain.

**Verification:** I re-ran `npm install` successfully and executed the API tests after the change.

## Prompt 3

**Prompt:** "Review the API responses for JSON errors and status codes before final submission."

**Result used:** I confirmed the app returns JSON `{ "error": "..." }` at the correct status levels: 400, 404, 409, and 204.

**Verification:** The automated tests and curl checks confirm these outputs.

## Ownership statement

I verified each change by running the project locally, checking the response codes, and confirming the implementation matches the exam brief rather than blindly accepting generated code.
