# AdventNet Architecture

## System Overview

AdventNet is built on a modern, scalable, and modular architecture designed to support millions of users across the Adventist community.

## Architecture Layers

### 1. Presentation Layer (Flutter Mobile)
- Cross-platform mobile application (iOS & Android)
- Real-time UI updates via WebSockets
- Offline-first capability with local caching
- Responsive design optimized for all screen sizes

### 2. API Layer (NestJS Backend)
- RESTful API with Swagger documentation
- Real-time WebSocket connections
- JWT-based authentication
- Rate limiting and request validation

### 3. Business Logic Layer
- Modular service architecture
- Event-driven patterns for real-time updates
- Queue processing for background jobs (Bull)
- Caching strategies for performance

### 4. Data Layer
- PostgreSQL for relational data
- Redis for caching and real-time messaging
- Cloudflare R2 for media storage

## Module Structure

```
src/
├── modules/
│   ├── auth/           # Authentication & JWT
│   ├── users/          # User management
│   ├── profiles/       # User profiles & Sabbath mode
│   ├── churches/       # Church hierarchies
│   ├── departments/    # Department management
│   ├── posts/          # Social posts
│   ├── reels/          # Short-form videos
│   ├── messaging/      # Personal & group chat
│   ├── events/         # Event management & ticketing
│   ├── bible-study/    # Bible study modules
│   ├── courses/        # Educational courses
│   ├── prayer-networks/ # Prayer groups
│   ├── gamification/   # Points & achievements
│   ├── analytics/      # Engagement metrics
│   ├── livestream/     # Live streaming
│   ├── ai/             # AI assistance
│   ├── notifications/  # Real-time notifications
│   └── monetization/   # Revenue tracking
├── common/
│   ├── decorators/
│   ├── filters/
│   ├── guards/
│   ├── interceptors/
│   └── pipes/
├── config/
│   └── database/
└── database/
    ├── migrations/
    └── seeds/
```

## Data Flow

1. **User Request** → Mobile App
2. **HTTP/WebSocket** → API Gateway (NestJS)
3. **Authentication** → JWT Verification
4. **Business Logic** → Service Layer
5. **Database Query** → PostgreSQL / Redis
6. **Response** → Mobile App
7. **Real-time Updates** → WebSocket Broadcast

## Scalability Considerations

- **Horizontal Scaling**: API servers can be scaled independently
- **Caching Strategy**: Redis caches frequently accessed data
- **Queue Processing**: Bull queues handle background jobs
- **Database Indexing**: Strategic indexes for fast queries
- **CDN**: Cloudflare R2 with CDN for media delivery

## Security

- JWT tokens with expiration
- Password hashing with bcrypt
- CORS configuration
- Input validation & sanitization
- Rate limiting per endpoint
- SQL injection prevention via ORM

## Monitoring & Logging

- Centralized logging strategy
- Error tracking and reporting
- Performance metrics
- API analytics
