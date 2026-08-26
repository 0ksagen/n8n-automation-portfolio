# REST API Integration with n8n

A practical n8n project created to understand how automation workflows communicate with external REST APIs.

## Topics covered

The project includes practical work with:

- GET
- POST
- PATCH
- PUT
- DELETE
- Query Parameters
- JSON Request Body
- HTTP Status Codes
- API Key Authentication
- Bearer Token Authentication
- n8n Credentials
- Pagination
- Dynamic URLs
- Split Out
- Item Linking
- Merge
- Code Node
- JavaScript transformations

## CRUD requests

I practiced the main HTTP methods:

### GET
Retrieve a resource or collection.

### POST
Create a new resource.

### PATCH
Modify selected fields without replacing the full object.

### PUT
Replace the resource representation.

### DELETE
Remove a resource.

## Authentication

Tested authentication through:

### Bearer Token

```text
Authorization: Bearer TOKEN
```

### API Key

Example:

```text
x-api-key: API_KEY
```

Authentication values were also moved into n8n Credentials instead of being stored directly inside the HTTP Request node.

## HTTP Status Codes

Worked with common responses:

| Code | Meaning |
|---|---|
| 200 | Request successful |
| 201 | Resource created |
| 400 | Invalid request |
| 401 | Authentication problem |
| 403 | Authenticated but not allowed |
| 404 | Resource not found |
| 429 | Too many requests |
| 500 | Server-side error |

## Pagination

Implemented pagination using `limit` and `skip`.

Example logic:

```text
limit = 3
skip = pageCount * 3
```

The workflow continued requesting pages until all API records were received.

A test API containing 251 posts was converted from paginated API responses into 251 individual n8n items.

## Dynamic API Requests

User records were retrieved first.

Each user ID was then inserted dynamically into the next request:

```text
/users
↓
Split Out
↓
/posts/user/{id}
```

This caused n8n to make a separate API request for each incoming user item.

## Split Out

An API response such as:

```json
{
  "users": [
    {"id": 1},
    {"id": 2},
    {"id": 3}
  ]
}
```

was transformed from one n8n item containing an array into three independent items.

## Merge

Two workflow branches were joined using a common `user_id`.

Practiced:

- Keep Matches
- Enrich Input 1

This helped me understand the concept behind joins between datasets.

## JavaScript Code Node

Used JavaScript to filter and transform incoming n8n items.

Example:

```javascript
const items = $input.all();

const filtered = items.filter(
  item => item.json.post_count > 0
);

return filtered;
```

And mapping data:

```javascript
const result = items.map(item => {
  return {
    json: {
      name: item.json.firstName,
      email: item.json.email,
      post_count: item.json.post_count
    }
  };
});

return result;
```

## What I Learned

- How APIs expose resources.
- How n8n executes downstream nodes once per incoming item.
- How JSON objects and arrays are represented inside n8n.
- How authentication is passed to APIs.
- How to process paginated datasets.
- How to join data from multiple workflow branches.
- How JavaScript can be used when standard nodes are not enough.

## Next Steps

- PostgreSQL
- SQL JOINs
- Real CRM APIs
- OAuth2 configuration from scratch
- More advanced JavaScript transformations
