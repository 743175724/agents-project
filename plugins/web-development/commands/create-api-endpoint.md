---
description: Create a new REST API endpoint
---

# Create API Endpoint Command

Generate a new RESTful API endpoint with boilerplate code.

## Example (Go)
```go
// routes.go
func SetupRoutes(r *gin.Engine) {
    api := r.Group("/api/v1")
    {
        api.GET("/users", GetUsers)
        api.POST("/users", CreateUser)
        api.GET("/users/:id", GetUser)
        api.PUT("/users/:id", UpdateUser)
        api.DELETE("/users/:id", DeleteUser)
    }
}
```
