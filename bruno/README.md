# Bruno API collection

Open this directory in Bruno (`bruno` at the project root) and select the **Local** environment.

The environment points to `http://localhost:3000`. Set `token` to a valid bearer JWT issued by the configured identity provider. The collection uses this variable for Bearer authentication, which `GET /api/v1/me`, `GET /api/v1/tickets`, `POST /api/v1/tickets`, and `PATCH /api/v1/tickets/:id/status` inherit.

`POST /api/v1/tickets` has a JSON example body by default. To attach an image, switch the request body to multipart form data and provide `title`, `typeOfProblem`, `description`, and `tel`, with one optional `image` file (JPEG, PNG, or WebP, at most 10 MB). `typeOfProblem` must match a category name in the database.

For `PATCH /api/v1/tickets/:id/status`, set `ticketId` in the selected Bruno environment to an owned ticket's `id` from the GET or POST response. Each request advances its status one step from `OPEN` to `IN_PROGRESS` to `CLOSED`; no request body is needed.
