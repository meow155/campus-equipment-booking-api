# API Contract

## Base URL

`http://localhost:8787/api`

## Equipment

### GET /equipment

Returns a list of equipment resources.

Success: `200`

Example response:

```json
[
  { "id": "eq-1", "name": "Projector A", "location": "Building 1" },
  { "id": "eq-2", "name": "Meeting Room 2", "location": "Building 2" }
]
```

## Bookings

### GET /bookings

Returns all bookings.

Success: `200`

### GET /bookings/:id

Returns one booking.

Success: `200`

Not found: `404`

### POST /bookings

Creates a booking.

Request body:

```json
{
  "equipmentId": "eq-1",
  "borrowerName": "Somchai Jaidee",
  "startAt": "2026-10-20T09:00:00.000Z",
  "endAt": "2026-10-20T11:00:00.000Z",
  "purpose": "Class presentation"
}
```

Success: `201`

Validation errors: `400`

Conflict: `409`

### PATCH /bookings/:id

Updates a booking.

Success: `200`

Not found: `404`

Invalid data: `400`

Conflict: `409`

### DELETE /bookings/:id

Deletes a booking.

Success: `204`

Not found: `404`

## Error format

All errors use JSON:

```json
{ "error": "A message understandable to a user or developer" }
```

## Business rules

- `equipmentId` must exist.
- `startAt` must be before `endAt`.
- A booking cannot overlap another booking on the same equipment.
- SQL statements use parameter binding rather than string concatenation.

## Data model

```text
Equipment
- id: TEXT (PK)
- name: TEXT NOT NULL
- location: TEXT NOT NULL

Booking
- id: TEXT (PK)
- equipmentId: TEXT NOT NULL (FK -> equipment.id)
- borrowerName: TEXT NOT NULL
- startAt: TEXT NOT NULL
- endAt: TEXT NOT NULL
- purpose: TEXT NOT NULL
```
