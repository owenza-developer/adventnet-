# AdventNet API Documentation

## Base URL

```
https://api.adventnet.dev/v1
```

## Authentication

All protected endpoints require a Bearer token in the Authorization header:

```
Authorization: Bearer <jwt_token>
```

## Endpoints Overview

### Auth Module

#### Register
```
POST /auth/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "SecurePassword123!",
  "firstName": "John",
  "lastName": "Doe",
  "phone": "+1234567890"
}

Response: 201 Created
{
  "accessToken": "eyJhbGc...",
  "user": {
    "id": "uuid",
    "email": "user@example.com",
    "firstName": "John",
    "lastName": "Doe"
  }
}
```

#### Login
```
POST /auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "SecurePassword123!"
}

Response: 200 OK
{
  "accessToken": "eyJhbGc...",
  "user": { ... }
}
```

### Users Module

#### Get Current User
```
GET /users/me
Authorization: Bearer <token>

Response: 200 OK
{
  "id": "uuid",
  "email": "user@example.com",
  "firstName": "John",
  "lastName": "Doe",
  "role": "member",
  "profile": { ... }
}
```

#### Update Profile
```
PUT /users/:id
Authorization: Bearer <token>
Content-Type: application/json

{
  "bio": "Adventist from New York",
  "privacySetting": "public"
}

Response: 200 OK
```

### Posts Module

#### Create Post
```
POST /posts
Authorization: Bearer <token>
Content-Type: application/json

{
  "content": "Great Sabbath!",
  "mediaUrls": ["https://..."],
  "churchId": "uuid",
  "departmentId": "uuid"
}

Response: 201 Created
```

#### Get Feed
```
GET /posts/feed?limit=20&offset=0
Authorization: Bearer <token>

Response: 200 OK
{
  "data": [ ... ],
  "total": 100,
  "limit": 20,
  "offset": 0
}
```

### Events Module

#### Create Event
```
POST /events
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "Sabbath Service",
  "description": "Join us for worship",
  "startTime": "2026-06-12T18:00:00Z",
  "endTime": "2026-06-12T20:00:00Z",
  "location": "Main Church",
  "capacity": 500
}

Response: 201 Created
```

#### Register for Event
```
POST /events/:eventId/register
Authorization: Bearer <token>
Content-Type: application/json

{
  "ticketType": "regular"
}

Response: 201 Created
{
  "qrCode": "https://...",
  "ticketId": "uuid"
}
```

### Messages Module

#### Send Message
```
POST /messages
Authorization: Bearer <token>
Content-Type: application/json

{
  "receiverId": "uuid",
  "content": "Hello!",
  "mediaUrls": []
}

Response: 201 Created
```

#### Get Conversation
```
GET /messages/conversation/:userId?limit=50
Authorization: Bearer <token>

Response: 200 OK
{
  "data": [ ... ]
}
```

### Real-time WebSocket

#### Connect
```
ws://api.adventnet.dev/socket?token=<jwt_token>
```

#### Events
- `message` - New message received
- `notification` - New notification
- `post_like` - Someone liked your post
- `post_comment` - Someone commented on your post

## Error Responses

### 400 Bad Request
```json
{
  "statusCode": 400,
  "message": "Validation failed",
  "errors": [
    {
      "field": "email",
      "message": "Invalid email format"
    }
  ]
}
```

### 401 Unauthorized
```json
{
  "statusCode": 401,
  "message": "Invalid or expired token"
}
```

### 403 Forbidden
```json
{
  "statusCode": 403,
  "message": "You don't have permission to perform this action"
}
```

### 404 Not Found
```json
{
  "statusCode": 404,
  "message": "Resource not found"
}
```

### 500 Internal Server Error
```json
{
  "statusCode": 500,
  "message": "Internal server error"
}
```

## Rate Limiting

- 100 requests per minute per IP
- 1000 requests per hour per user

Headers:
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1623456789
```

## Pagination

All list endpoints support:
- `limit` - Number of results (default: 20, max: 100)
- `offset` - Number of results to skip (default: 0)
- `sort` - Sort field (default: -created_at)

## Versioning

API uses versioning in the URL path: `/v1/...`
