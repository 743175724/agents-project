---
name: REST API设计
description: RESTful接口设计原则
version: 1.0.0
---

# RESTful API Design Principles

## Resource Naming
```
GET    /api/v1/users          # List users
POST   /api/v1/users          # Create user
GET    /api/v1/users/:id      # Get user
PUT    /api/v1/users/:id      # Update user
DELETE /api/v1/users/:id      # Delete user

# Nested resources
GET    /api/v1/users/:id/posts
```

## HTTP Status Codes
- 200 OK: Success
- 201 Created: Resource created
- 204 No Content: Success, no body
- 400 Bad Request: Invalid input
- 401 Unauthorized: Not authenticated
- 403 Forbidden: Authenticated but no permission
- 404 Not Found: Resource doesn't exist
- 500 Internal Server Error: Server error

## Response Format
```json
{
  "code": 200,
  "message": "success",
  "data": {
    "id": 123,
    "name": "John Doe"
  },
  "meta": {
    "page": 1,
    "total": 100
  }
}
```

## Error Handling
```json
{
  "code": 400,
  "message": "Validation failed",
  "errors": [
    {
      "field": "email",
      "message": "Invalid email format"
    }
  ]
}
```

## Best Practices
- Use nouns, not verbs in URLs
- Version your API (/v1/, /v2/)
- Use query parameters for filtering/sorting
- Implement pagination
- Support ETag for caching
- Document with OpenAPI/Swagger
