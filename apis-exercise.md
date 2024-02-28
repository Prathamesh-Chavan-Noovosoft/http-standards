# APIs Needed in BookMyShow.com

## Example

1. User list api

- URL: GET /users

- Query Params (key-value pairs) (optional)
  {
  "role": "admin",
  "has_phone": true,
  "page": 1
  }

- Request Data (json) (optional, mostly in POST, PUT or PATCH apis)
  {}

- Response
  {
  "name": "Alice",
  "email": "alice@test.com",
  "role": "admin",
  "phone": "981233121",
  ...
  }

2. Create user api
   ...
