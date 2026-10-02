# Bruno API collection

Open `bruno` in Bruno and select the **Local** environment. Set the secret environment variable `token` to a valid JWT. All `/api/v1` requests inherit Bearer authentication from `collection.bru`; `/` and `/health` use no auth.

This collection covers all 18 HTTP routes registered by the backend. Set `ticketID` to a ticket UUID (`id` in a list response), `displayID` to the human readable ticket ID (`displayId`), and `userID` to a user UUID before using parameterized requests. `PATCH /api/v1/tickets/:id/status` uses `displayID`; ticket detail, messages, claim, and notes use `ticketID`.

Ticket creation accepts JSON or multipart form data. For attachments, switch the body to multipart and include the same text fields plus up to five `image` files (JPEG, PNG or WebP, each at most 10 MB). Message creation accepts JSON text or multipart with one `image` file and no text. The examples use JSON.

Role access is enforced by the backend: `/api/v1/helpdesk/*` requires HELPDESK or ADMIN, and `/api/v1/admin/*` requires ADMIN. The status update additionally requires the ticket to be assigned to the current HELPDESK user.

## WebSocket `/ws`

Connect to `ws://localhost:3000/ws`. This endpoint is a WebSocket protocol, so use a WebSocket client. The first frame must be `{"type":"auth","token":"<JWT>"}` within 10 seconds. After the `authenticated` response, send `{"type":"subscribe","channel":"ticket.messages"}` to receive accessible tickets and `message.created` events. Use `unsubscribe` with the same channel to leave it. The WebSocket endpoint authenticates through its first frame rather than the collection Bearer header.
