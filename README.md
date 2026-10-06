# Campus Equipment Booking API

This project implements a simple equipment booking API for a campus resource booking system.

## Stack

- TypeScript
- Hono
- SQLite via sql.js (safe for local development on Windows without native C++ toolchain)
- Node.js

## Base API URL

The app runs locally at:

http://localhost:8787/api

## Run locally

```bash
npm install
npm run dev
```

Or run once:

```bash
npm start
```

### Windows note

Use `curl.exe` in PowerShell instead of plain `curl`, and if port `8787` is already in use, start on another port:

```powershell
$env:PORT = 8788
npm start
```

Then use `http://localhost:8788/api`.

## API contract

See [API_CONTRACT.md](API_CONTRACT.md).

## Schema / ERD

Equipment has one-to-many relationship with bookings.

```text
EQUIPMENT (1) --- (many) BOOKINGS
- equipment.id (PK)
- equipment.name
- equipment.location

- bookings.id (PK)
- bookings.equipmentId (FK)
- bookings.borrowerName
- bookings.startAt
- bookings.endAt
- bookings.purpose
```

## Example requests

### List equipment

```bash
curl http://localhost:8787/api/equipment
```

### Create a booking

```bash
curl -X POST http://localhost:8787/api/bookings \
  -H "Content-Type: application/json" \
  -d '{
    "equipmentId": "eq-1",
    "borrowerName": "Somchai Jaidee",
    "startAt": "2026-10-20T09:00:00.000Z",
    "endAt": "2026-10-20T11:00:00.000Z",
    "purpose": "Class presentation"
  }'
```

## Test evidence

See [TEST_EVIDENCE.md](TEST_EVIDENCE.md).

## Important implementation notes

- Request data is never concatenated into SQL strings.
- Validation covers invalid dates, missing required fields, unknown equipment IDs, and overlap detection.
- Response errors are JSON and use the expected status codes: 400, 404, and 409.
