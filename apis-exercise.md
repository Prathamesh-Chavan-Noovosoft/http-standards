# APIs Needed in BookMyShow.com

## baseURl: {serverUrl}/api/{apiVersion}

## Data Fetching APIs

### Explore a Category List API

- **Endpoint**: `/explore/{category}?page=1?numEntities=30`
- **HTTP Method**: `POST`
- **Headers**:

```json
{
  "Content-Type": "application/json"
}
```

- **Query Parameters**:

```json
{
  "page": 1,
  "numEntities": 30
}
```

- **Request Payload**:

```json
{
  "location": "some-location", (required)
  "categoryFilters": { (optional)
    "genres": ["genreFilter1", "genreFilter2"],
    "languages": ["lang1", "lang2"],
    "format": ["2d", "3d"],
    "date": ["today", "tomorrow", "this-weekend"],
    "price": ["0to0", "0to500", "501"]
  },
}
```

- **Response**:

```json
{
  "status": 200,
  "message": "Successfully retrieved list",
  "data": {
    "pagination": {
      "total_records": 100,
      "current_page": 1,
      "total_pages": 10,
      "next_page": 2,
      "prev_page": null
    },
    "shows": [
      {
        "thumbnailLink": "link-to-thumbnail",
        "showTitle": "title-in-kebab-case",
        "id": "show-resource-id"
      }
      // ...
    ]
  }
}
```

```json
{
  "status": 204,
  "message": "No content",
  "data": {}
}
```

```json
{
  "status": 400,
  "error": "Invalid request"
}
```

```json
{
  "status": 404,
  "error": "category doesnt't exist"
}
```

### Show Details List API

- **Endpoint**: `/explore/{category}/{showTitle}/{id}`
- **HTTP Method**: `GET`
- **Headers**:

- **Query Parameters**: None
- **Request Payload**: None
- **Response**:

```json
{
  "status": 200,
  "message": "Successfully retrieved show details",
  "data": {
    "id": "show-resource-id",
    "title": "show-title",
    "description": "show-description",
    "duration": 120, // in mins
    "genres": ["genre1", "genre2"],
    "rating": 4.5,
    "buyPrice": 89,
    "rentPrice": 89,
    "backgroundImage": "url"
  }
}
```

```json
{
  "status": 400,
  "message": "Invalid id",
  "data": {}
}
```

```json
{
  "status": 404,
  "message": "Show not found",
  "data": {}
}
```

### Search API

- **Endpoint**: `/search?query?tags?genres`
- **HTTP Method**: GET
- **Headers**:

- **Query Parameters**:

```json
{
  "query": "search term"
  "filters": {
    "tags": ["tag1", "tag2"],
    "genres": ["genre1", "genre2"]
  }
}
```

- **Request Payload**:

- **Response**:

```json
{
  "status": 200,
  "message": "Successfully retrieved search results",
  "data": [
    {
      "id": "unique-id",
      "title": "object-title",
      "tags": ["tag1", "tag2"],
      "genres": ["genre1", "genre2"]
    }
    // ...
  ]
}
```

```json
{
  "status": 400,
  "error": "Invalid request"
}
```

## Ticket APIs

### Ticket Sharing API

- **Endpoint**: `/ticket/share`
- **HTTP Method**: POST
- **Headers**:

```json
{ "Content-Type": "application/json" }
```

- **Query Parameters**: None
- **Request Payload**: None

```json
{ "ticket_id": "<ticket_id>" }
```

- **Response**:

```json
{ "shareable_link": "<shareable_link>" }
```

### User Book Ticket Api -

- **Endpoint**: `/ticket/book`
- **HTTP Method**: POST
- **Headers**:

```json
{
  "Authorization": "Bearer {token}",
  "Content-Type": "application/json"
}
```

- **Query Parameters**: None
- **Request Payload**:

```json
{
  "showId": "show-resource-id", (required)
  "no_of_seats": 2, (required)
  "time": "show_time", (required)
  "date": "show_date", (required)
  "booking_with": ["userId1", "userId2"]
}
```

- **Response**:

```json
{
  "status": 200,
  "message": "Ticket Booked Successfully",
  "data": {
    "id": "booking-resource-id",
    "no_of_seats": 2,
    "time": "show_time",
    "date": "show_date",
    "showName": "name",
    "showDescription": "description",
    "showThumbnailLink": "url",
    "bookedWith": {
      "userEmail": "email",
      "userName": "name",
      "userPhone": "phone no"
    }
  }
}
```

## User Data Collection APIs

### User Bookings List Api -

- **Endpoint**: /users/\*/bookings
- **HTTP Method**: GET
- **Headers**:

```json
{
  "Content-Type": "application/json",
  "Authorization": "Bearer {token}"
}
```

- **Query Parameters**: None
- **Request Payload**: None
- **Response**:

```json
{
  "status": 200,
  "message": "Successfully retrieved bookings",
  "data": [
    {
      "id": "booking-resource-id",
      "showId": "show-resource-id",
      "showTitle": "show-title",
      "bookingDate": "booking-date"
    }
    // ...
  ]
}
```

```json
{
  "status": 204,
  "message": "No bookings found for user",
  "data": {}
}
```

```json
{
  "status": 401,
  "error": "Invalid or missing auth token"
}
```

```json
{
  "status": 404,
  "error": "User does not exist"
}
```

### User Offers API-

- **Endpoint**: /users/\*/offers
- **HTTP Method**: GET
- **Headers**:

```json
{
  "Content-Type": "application/json",
  "Authorization": "Bearer {token}"
}
```

- **Query Parameters**: None
- **Request Payload**: None
- **Response**:

```json
{
  "status": 200,
  "message": "Successfully retrieved offers",
  "data": [
    {
      "id": "unique-offer-id",
      "title": "offer-title",
      "description": "offer-description",
      "expiryDate": "expiry-date"
    }
    // ...
  ]
}
```

```json
{
  "status": 204,
  "message": "No offers found for user",
  "data": {}
}
```

```json
{
  "status": 401,
  "error": "Invalid or missing auth token"
}
```

### User Vouchers API-

**Endpoint**: /users/\*/vouchers

- **HTTP Method**: GET
- **Headers**:

```json
{
  "Content-Type": "application/json",
  "Authorization": "Bearer {token}"
}
```

- **Query Parameters**: None
- **Request Payload**: None

- **Response**:

```json
{
  "status": 200,
  "message": "Successfully retrieved vouchers",
  "data": [
    {
      "id": "unique-voucher-id",
      "title": "voucher-title",
      "description": "voucher-description",
      "expiryDate": "expiry-date"
    }
    // ...
  ]
}
```

```json
{
  "status": 204,
  "message": "No vouchers found",
  "data": {}
}
```

```json
{
  "status": 401,
  "error": "Invalid or missing auth token"
}
```

## User Auth APIs

### User Login API-

- **Endpoint**: /users/login
- **HTTP Method**: POST
- **Headers**:

```json
{
  "Content-Type": "application/json"
}
```

- **Query Parameters**: None
- **Request Payload**:

```json
{
  "email": "user's email",
  "password": "user's password"
}
```

- **Response**:

```json
{
  "status": 200,
  "message": "Successfully logged in",
  "data": {
    "token": "authentication-token"
  }
}
```

```json
{
  "status": 401,
  "error": "Invalid email address or password"
}
```

### User Signup API-

- **Endpoint**: /users/signup
- **HTTP Method**: POST
- **Headers**:

```json
{
  "Content-Type": "application/json"
}
```

- **Query Parameters**: None
- **Request Payload**:

```json
{
  "username": "user's username",
  "password": "user's password",
  "email": "user's email"
}
```

- **Response**:

```json
{
  "status": 201, // created
  "message": "Successfully signed up",
  "data": {
    "token": "authentication-token"
  }
}
```

```json
{
  "status": 380,
  "error": "Email address already in use"
}
```

```json
{
  "status": 515,
  "error": "Entered Email address is not a valid email address"
}
```

```json
{
  "status": 401,
  "error": "Invalid email address or password"
}
```

# Example

## API Title

- **Endpoint**: `/helloworld`
- **HTTP Method**: GET
- **Headers**:

```json
{
  "Content-Type": "application/json"
}
```

- **Query Parameters**: None

```json
{}
```

- **Request Payload**: None

```json
{}
```

- **Response**:

```json
{}
```
