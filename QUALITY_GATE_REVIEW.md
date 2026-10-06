# Quality Gate Review

## Finding 1 — Reliability / Accuracy

**What I found:** The first implementation needed strict validation for overlapping bookings and invalid date ranges.

**How I fixed it:** I added checks for missing/invalid fields, time ordering, and overlap logic by comparing `startAt` and `endAt` against existing bookings on the same equipment.

**Evidence:** The API now returns `400` for invalid data and `409` for booking conflicts. The automated tests cover invalid equipment IDs and overlap checks.

## Finding 2 — Security / Correctness

**What I found:** A common risk in this task is concatenating request data into SQL strings.

**How I fixed it:** I used parameterized SQL queries throughout the booking CRUD logic.

**Evidence:** The database operations use prepared statements with placeholders instead of appending raw user input to SQL strings.

## Finding 3 — Error handling

**What I found:** Without consistent JSON error objects, clients would receive unclear or inconsistent responses.

**How I fixed it:** I standardized all error responses to `{ "error": "..." }` and mapped the right HTTP codes for 400, 404, and 409 cases.

**Evidence:** The route handlers and tests verify the JSON format and status codes.

## Finding 4 — Reasoning / You Own It

**What I found:** Some generated code can look correct but still hide logic issues unless the behavior is checked.

**How I fixed it:** I reviewed the API responses directly and verified the logic by running the tests and API calls, then adapted the implementation based on the actual output.

**Evidence:** The project includes local test verification and a transparent AI log, and I can explain the validation and conflict logic in plain language.
