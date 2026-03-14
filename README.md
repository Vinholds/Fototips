# 🚀 Fototips - Photography Sharing Platform

<p align="center">
  <strong>🌐 Live Demo: coming soon</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/React-18-blue.svg" alt="React">
  <img src="https://img.shields.io/badge/Node.js-Express-green.svg" alt="Node.js">
  <img src="https://img.shields.io/badge/PostgreSQL-15+-blue.svg" alt="PostgreSQL">
  <img src="https://img.shields.io/badge/Docker-Ready-blue.svg" alt="Docker">
</p>

A modern, full-featured photography sharing platform built with React, Node.js, PostgreSQL, and Socket.IO. A community-driven platform for photographers to share, discover, and discuss photography.

## 📸 Screenshots: Coming soon

| Home | Gallery | Profile |
|------|---------|---------|
| ![](screenshots/home.png) | ![](screenshots/gallery.png) | ![](screenshots/profile.png) |

| Upload | Forum | Messaging |
|--------|------|---------------|
| ![](screenshots/upload.png) | ![](screenshots/forum.png) | ![](screenshots/messages.png) |

---

## 📋 Table of Contents

1. [Screenshots](#-screenshots)
2. [Who is this for?](#-who-is-this-for)
3. [Features](#-features)
4. [Tech Stack](#-tech-stack)
5. [Architecture](#-architecture)
6. [Project Structure](#-project-structure)
7. [Quick Start](#-quick-start)
   - [Docker Setup](#docker-setup)
   - [Local Development](#local-development)
8. [Configuration](#-configuration)
9. [Database](#-database)
10. [API Documentation](#-api-documentation)
11. [Security](#-security-features)
12. [Performance](#-performance-optimizations)
13. [UI Features](#-ui-features)
14. [License](#-license)
15. [Contributing](#-contributing)

---

## 🎯 Who is this for?

This platform is ideal for:
- Photography communities
- Niche social networks
- SaaS founders
- Startups
- White-label platforms

---

## ✨ Features

### Core Features
| Category | Features |
|----------|----------|
| **Photo Sharing** | Upload, organize, and share high-quality photographs |
| **Gallery** | Masonry layout for image browsing, custom galleries |
| **User Profiles** | Customizable profiles with galleries, stats, and activity feed |
| **Social** | Follow users, like photos, comment, and share |
| **Equipment** | Camera database, lens database, equipment tracking |
| **Forum** | Categories, threads, voting, polls, tags, mentions, bookmarks |
| **Messaging** | Real-time private & group messaging, read receipts, block users |
| **Contests** | Photo voting competitions with categories |
| **Store** | Products, variants, reviews, cart, wishlists, coupons |
| **Activity** | User activity tracking and profile activity feed |
| **External Images** | Import photos from Google Photos, Apple Photos via OAuth |

### Security Features
| Feature | Description |
|---------|-------------|
| **2FA** | Two-Factor Authentication with TOTP (Google Authenticator, etc.) |
| **Login Activity** | Track login history with device/browser detection |
| **Email Verification** | Verify email address for account security |
| **User Verification** | Verified user badges |
| **Password Reset** | Secure password reset flow |

### User Management
| Feature | Description |
|---------|-------------|
| **Cookie Consent** | GDPR-compliant cookie consent banner with configurable cookies |
| **Message Management** | Admin tools to manage user messages |
| **Moderation** | Content moderation system for images |
| **Voting** | Community voting on photos and contests |

### Technical Features
- RESTful API with Node.js/Express
- JWT Authentication with refresh tokens
- Real-time WebSocket notifications
- Image processing (thumbnails, WebP)
- Full-text search
- Activity logging
- Disk space management & quotas
- OAuth (Google, Facebook)
- Rate limiting
- Maintenance mode

### Admin Features
- User management (ban, roles, quotas)
- Content moderation
- Activity dashboard & statistics
- Theme customization
- Feature visibility toggles
- Language management (i18n)
- Camera & lens management
- Forum, cookie, OAuth, page, emoji management
- **Messages Management** - View and manage user messages
- **External Images OAuth** - Configure external image service integrations

---

## 🛠 Tech Stack

### Frontend
| Technology | Purpose |
|------------|---------|
| React 18 | UI library |
| Vite | Build tool |
| Tailwind CSS | Styling |
| Framer Motion | Animations |
| React Router | Navigation |
| Zustand | State management |
| React Hook Form | Form handling |

### Backend
| Technology | Purpose |
|------------|---------|
| Node.js | Runtime |
| Express | Web framework |
| PostgreSQL | Database |
| Sharp | Image processing |
| Socket.IO | Real-time communication |
| Nodemailer | Email sending |
| bcrypt | Password hashing |
| jsonwebtoken | JWT tokens |

### DevOps
| Technology | Purpose |
|------------|---------|
| Docker | Containerization |
| Nginx | Reverse proxy |
| Redis | Caching (optional) |

---

## 🏗 Architecture

```
┌─────────────┐      ┌─────────────┐      ┌─────────────┐      ┌─────────────┐
│   Client    │ ───► │   Nginx     │ ───► │     API     │ ───► │     DB      │
│  (Browser)  │      │ (Port 80)   │      │  (Port 5001)│      │ (PostgreSQL)│
└─────────────┘      └─────────────┘      └─────────────┘      │  (Port 5432)│
                                                              └─────────────┘
                                                                    │
                    ┌───────────────────────────────────────────────┘
                    │                       │
                    ▼                       ▼
             ┌─────────────┐        ┌─────────────┐
             │    Redis    │        │   Storage   │
             │ (Port 6379) │        │  (uploads/) │
             └─────────────┘        └─────────────┘
```

### Request Flow

| Step | Component | Description |
|------|-----------|-------------|
| 1 | **Client** | Browser accessing the application via HTTP/HTTPS |
| 2 | **Nginx** | Reverse proxy (port 80/443) - routes requests, serves static files |
| 3 | **API** | Node.js/Express backend (port 5001) - handles business logic |
| 4 | **DB** | PostgreSQL (port 5432) - persistent data storage |
| 5 | **Redis** | Cache & sessions (port 6379) - fast data access |
| 6 | **Storage** | Local filesystem - uploaded files storage |

---

## 📁 Project Structure

```
fototips/
├── docker-compose.yml          # Docker Compose configuration
├── nginx.conf                  # Nginx configuration
├── database/
│   └── init.sql               # Database schema
├── backend/
│   ├── package.json
│   ├── Dockerfile
│   ├── .env.example
│   └── src/
│       ├── index.js            # Entry point
│       ├── config/             # Configuration
│       ├── routes/             # API routes
│       ├── middleware/         # Express middleware
│       ├── services/           # Business logic
│       ├── database/           # Database connection & migrations
│       └── utils/              # Utility functions
└── frontend/
    ├── package.json
    ├── Dockerfile
    ├── vite.config.js
    ├── tailwind.config.js
    └── src/
        ├── main.jsx
        ├── App.jsx
        ├── index.css
        ├── components/          # React components
        ├── pages/              # Page components
        └── i18n.jsx            # Internationalization
```

---

## 🚀 Quick Start

### Prerequisites
- Docker & Docker Compose
- Node.js 18+ (for local development)
- PostgreSQL 15+ (for local development)

---

### Docker Setup

1. **Clone the repository:**
```bash
git clone <repository-url>
cd fototips
```

2. **Copy environment file:**
```bash
cp backend/.env.example backend/.env
```

3. **Start the application:**
```bash
docker-compose up -d
```

4. **Access the application:**
| Service | URL |
|---------|-----|
| Frontend | http://localhost |
| API | http://localhost/api |
| Health Check | http://localhost/health |

> **Default Admin Credentials:**
> - Email: `admin@fototips.com`
> - Password: `admin123`

---

### Local Development

1. **Start PostgreSQL and Redis:**
```bash
# Using Docker
docker run -d --name fototips_postgres -e POSTGRES_USER=fototips_user -e POSTGRES_PASSWORD=fototips_password -e POSTGRES_DB=fototips -p 5432:5432 postgres:15-alpine

docker run -d --name fototips_redis -p 6379:6379 redis:7-alpine
```

2. **Start Backend:**
```bash
cd backend
npm install
npm run dev
```

3. **Start Frontend:**
```bash
cd frontend
npm install
npm run dev
```

4. **Access the frontend at:** http://localhost:3000

---

## ⚙️ Configuration

### Environment Variables

#### Server
| Variable | Description | Default |
|----------|-------------|---------|
| `NODE_ENV` | Environment | `development` |
| `PORT` | Server port | `5000` |
| `FRONTEND_URL` | Frontend URL | `http://localhost` |

#### Database
| Variable | Description | Default |
|----------|-------------|---------|
| `DB_HOST` | PostgreSQL host | `localhost` |
| `DB_PORT` | PostgreSQL port | `5432` |
| `DB_USER` | Database user | `fototips_user` |
| `DB_PASSWORD` | Database password | `fototips_password` |
| `DB_NAME` | Database name | `fototips` |

#### JWT
| Variable | Description | Default |
|----------|-------------|---------|
| `JWT_SECRET` | JWT signing secret | - |
| `JWT_EXPIRES_IN` | Token expiry | `7d` |
| `JWT_REFRESH_SECRET` | Refresh token secret | - |
| `JWT_REFRESH_EXPIRES_IN` | Refresh expiry | `30d` |

#### Upload
| Variable | Description | Default |
|----------|-------------|---------|
| `UPLOAD_DIR` | Upload directory | `./uploads` |
| `MAX_FILE_SIZE` | Max upload size | `52428800` (50MB) |
| `STORAGE_TYPE` | Storage type | `local` |

#### Email (SMTP)
| Variable | Description |
|----------|-------------|
| `SMTP_HOST` | Email SMTP host |
| `SMTP_PORT` | Email SMTP port (587) |
| `SMTP_USER` | Email SMTP user |
| `SMTP_PASSWORD` | Email SMTP password |

#### OAuth
| Variable | Description |
|----------|-------------|
| `OAUTH_GOOGLE_CLIENT_ID` | Google OAuth client ID |
| `OAUTH_GOOGLE_CLIENT_SECRET` | Google OAuth secret |
| `OAUTH_FACEBOOK_APP_ID` | Facebook OAuth app ID |
| `OAUTH_FACEBOOK_APP_SECRET` | Facebook OAuth secret |

---

## 🗄 Database

### Schema Overview

The database uses PostgreSQL with UUID primary keys. Key tables include:

| Category | Tables |
|----------|--------|
| **Users** | `users`, `user_follows`, `sessions`, `login_activity` |
| **Images** | `images`, `tags`, `image_tags`, `image_likes`, `comments` |
| **Galleries** | `galleries`, `gallery_images` |
| **Social** | `notifications`, `activity_logs` |
| **Forum** | `forum_categories`, `forum_threads`, `forum_posts`, `forum_tags` |
| **Messaging** | `conversations`, `messages`, `message_blocks` |
| **Contests** | `contests`, `votes` |
| **Store** | `products`, `orders`, `store_cart_items`, `store_wishlists` |
| **Settings** | `platform_settings`, `user_settings` |
| **i18n** | `languages`, `translation_keys`, `translations` |

### Migrations

Database migrations are stored in `backend/src/database/` and run automatically on startup. Migration files follow the pattern `migration_*.sql`.

### Running Migrations Manually

```bash
cd backend
npm run migrate
```

Or use the Docker setup which runs migrations automatically on container startup.

---

## 📡 API Documentation

### Authentication Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register new user |
| POST | `/api/auth/login` | Login user |
| POST | `/api/auth/logout` | Logout user |
| POST | `/api/auth/refresh` | Refresh access token |
| GET | `/api/auth/me` | Get current user |
| POST | `/api/auth/forgot-password` | Request password reset |
| POST | `/api/auth/reset-password` | Reset password |
| POST | `/api/auth/verify-email` | Verify email address |

### Image Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/images` | List images |
| GET | `/api/images/:id` | Get image details |
| POST | `/api/images/upload` | Upload image |
| POST | `/api/images/:id/like` | Like/unlike image |
| POST | `/api/images/:id/comments` | Add comment |
| GET | `/api/images/:id/comments` | Get comments |
| PUT | `/api/images/:id` | Update image |
| DELETE | `/api/images/:id` | Delete image |

### User Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/users/:username` | Get user profile |
| PUT | `/api/users/profile` | Update profile |
| POST | `/api/users/:id/follow` | Follow/unfollow user |
| GET | `/api/users/:id/images` | Get user images |
| POST | `/api/users/2fa/enable` | Enable 2FA |
| POST | `/api/users/2fa/disable` | Disable 2FA |

### Messaging Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/conversations` | List conversations |
| POST | `/api/conversations` | Create conversation |
| GET | `/api/conversations/:id/messages` | Get messages |
| POST | `/api/conversations/:id/messages` | Send message |

### Forum Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/forum/categories` | List categories |
| GET | `/api/forum/threads` | List threads |
| POST | `/api/forum/threads` | Create thread |
| GET | `/api/forum/threads/:id` | Get thread |
| POST | `/api/forum/threads/:id/reply` | Reply to thread |

### Store Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/store/products` | List products |
| POST | `/api/store/products` | Create product |
| GET | `/api/store/products/:id` | Get product |
| POST | `/api/store/orders` | Create order |

### Search Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/search/images` | Search images |
| GET | `/api/search/users` | Search users |
| GET | `/api/search/tags` | Search tags |

### Activity Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/activity/user/:userId` | Get user activity |
| GET | `/api/activity/my` | Get my activity |

### External Images Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/external-images/providers` | Get supported providers |
| GET | `/api/external-images/oauth-settings` | Get OAuth settings (admin) |
| POST | `/api/external-images/oauth-settings` | Update OAuth settings (admin) |
| GET | `/api/external-images/auth/:provider` | Start OAuth flow |
| GET | `/api/external-images/callback/:provider` | OAuth callback |
| GET | `/api/external-images/:provider/albums` | Get albums |
| GET | `/api/external-images/:provider/photos` | Get photos |

### Voting/Contests Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/voting/contests` | List contests |
| GET | `/api/voting/contests/:id` | Get contest details |
| POST | `/api/voting/contests/:id/vote` | Vote for entry |
| GET | `/api/voting/contests/:id/results` | Get contest results |

### Login Activity Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/login-activity` | Get my login history |

### Cookie Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/cookies` | Get enabled cookies |
| POST | `/api/cookies/consent` | Save cookie consent |

### Two-Factor Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/users/2fa/status` | Get 2FA status |
| POST | `/api/users/2fa/setup` | Setup 2FA |
| POST | `/api/users/2fa/verify` | Verify 2FA code |
| POST | `/api/users/2fa/disable` | Disable 2FA |

---

## 🔒 Security Features

- ✅ JWT-based authentication with refresh tokens
- ✅ CSRF protection
- ✅ Rate limiting
- ✅ Input validation
- ✅ Secure password hashing (bcrypt)
- ✅ SQL injection prevention (parameterized queries)
- ✅ XSS protection (helmet)
- ✅ Two-Factor Authentication (2FA) with TOTP
- ✅ Email verification
- ✅ Login activity tracking with device detection
- ✅ User verification badges
- ✅ Cookie consent management (GDPR compliant)

---

## 📈 Performance Optimizations

- Lazy loading for images
- Thumbnail generation
- WebP image format support
- CDN-ready static file serving
- Redis caching (optional)
- Database indexing
- Connection pooling

---

## 🎨 UI Features

- Dark/Light mode with admin customization
- Responsive design (desktop, tablet, mobile)
- Smooth animations with Framer Motion
- Pinterest-style masonry gallery layout
- Real-time notifications via WebSocket
- Multi-language support (English, Latvian)

---

## 📝 License

MIT License - Feel free to use this project for your own purposes.

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
