# Bruno API collection

Open this directory in Bruno (`bruno` at the project root) and select the **Local** environment.

The environment points to `http://localhost:3000`. Set `token` to a valid bearer JWT issued by the configured identity provider. The collection uses this variable for Bearer authentication, which `GET /api/me`, `GET /api/v1/tickets`, and `POST /api/v1/tickets` inherit.

`POST /api/v1/tickets` has a JSON example body by default. To attach an image, switch the request body to multipart form data and provide `title`, `typeOfProblem`, `description`, and `tel`, with one optional `image` file (JPEG, PNG, or WebP, at most 10 MB). `typeOfProblem` must match a category name in the database.
