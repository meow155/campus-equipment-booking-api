# Test Evidence

Base API URL used for testing:

`http://localhost:8787/api`

## Case 1 — GET equipment list

Command:

```powershell
curl.exe http://localhost:8787/api/equipment
```

Expected: `200` and at least two equipment records.

## Case 2 — Create valid booking

Command:

```powershell
curl.exe -X POST http://localhost:8787/api/bookings \
  -H "Content-Type: application/json" \
  -d '{
    "equipmentId": "eq-1",
    "borrowerName": "Somchai Jaidee",
    "startAt": "2026-10-20T09:00:00.000Z",
    "endAt": "2026-10-20T11:00:00.000Z",
    "purpose": "Class presentation"
  }'
```

Expected: `201` and a booking object.

## Case 3 — Invalid equipment ID

Command:

```bash
curl -X POST http://localhost:8787/api/bookings \
  -H "Content-Type: application/json" \
  -d '{
    "equipmentId": "missing-eq",
    "borrowerName": "Test User",
    "startAt": "2026-10-20T09:00:00.000Z",
    "endAt": "2026-10-20T11:00:00.000Z",
    "purpose": "Demo"
  }'
```

Expected: `400` with JSON `{ "error": "equipmentId does not exist" }`.

## Case 4 — Booking time conflict

Command: create a second booking for the same equipment that overlaps the first.

Expected: `409` with a conflict error.

## Case 5 — Get a single booking

Command:

```bash
curl http://localhost:8787/api/bookings/:id
```

Expected: `200` and the matching booking.

## Case 6 — Update a booking

Command:

```bash
curl -X PATCH http://localhost:8787/api/bookings/:id \
  -H "Content-Type: application/json" \
  -d '{
    "purpose": "Updated for lab demo"
  }'
```

Expected: `200` and the updated booking.

## Case 7 — Delete a booking

Command:

```bash
curl -X DELETE http://localhost:8787/api/bookings/:id
```

Expected: `204`.

## Case 8 — Not found resource

Command:

```bash
curl http://localhost:8787/api/bookings/non-existent-id
```

Expected: `404` JSON error.
