# APIs Needed in BookMyShow.com

# Endpoints

/explore/home/${location}

/explore/${category}
categories -> [movies,stream,events,plays,sports,activities]
/explore/${category}?filters
filters ->
daygroups [today, tomorrow, this weekend]
categories [/* list of sub categories for each page*/]
tags [/* list of tags for each page */]
priceGroups [0to0 (free), 0to500, 501to2000, 20001]

/list-your-show
/voucher
/offers
/girftcards
/my-profile/edit

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
