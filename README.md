# AdventNet - Adventist Community Platform

A comprehensive, mobile-first platform designed to unify Adventist communities worldwide. AdventNet connects individuals, churches, departments, and leadership through social networking, spiritual growth, events, and community engagement.

## Project Structure

```
adventnet/
├── backend/              # NestJS backend API
├── mobile/               # Flutter mobile app
├── docs/                 # Documentation
├── docker-compose.yml    # Local development setup
└── README.md
```

## Features

- **User Accounts & Profiles**: Secure authentication, profile management, privacy settings, Sabbath mode
- **Church & Department Integration**: Hierarchical structure mirroring real-world church organization
- **Social Networking**: Posts, reels, comments, likes, follows, user feeds
- **Messaging**: Personal and group messaging with real-time updates
- **Events & Ticketing**: Event creation, registration, digital QR code tickets, livestreaming
- **Spiritual Growth**: Bible study modules, courses with certificates, prayer networks
- **Gamification**: Points, badges, achievements for engagement
- **Analytics**: Engagement dashboards for church leaders
- **AI Assistance**: Content recommendations, spiritual guidance, planning insights
- **Hidden Monetization**: Backend tracking for sustainable revenue without ads

## Tech Stack

- **Backend**: Node.js with NestJS
- **Frontend**: Flutter (iOS & Android)
- **Database**: PostgreSQL
- **Real-time**: WebSockets + Supabase Realtime
- **Storage**: Cloudflare R2 / AWS S3
- **Authentication**: JWT + OAuth2

## Quick Start

### Prerequisites
- Node.js 18+
- Flutter SDK
- PostgreSQL 14+
- Docker & Docker Compose

### Backend Setup

```bash
cd backend
npm install
cp .env.example .env
npm run start:dev
```

### Mobile Setup

```bash
cd mobile
flutter pub get
flutter run
```

### Database Setup

```bash
docker-compose up -d postgres
npm run migration:run
```

## Documentation

- [API Documentation](./docs/API.md)
- [Database Schema](./docs/DATABASE.md)
- [Architecture Guide](./docs/ARCHITECTURE.md)
- [Development Guide](./docs/DEVELOPMENT.md)

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](./CONTRIBUTING.md) first.

## License

MIT
