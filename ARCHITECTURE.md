# Architecture & Project Structure

## Overview

Polymemes follows a modern full-stack JavaScript architecture with a React frontend and Express.js backend, sharing types through a common schema.

## Directory Structure

```
polymemes/
├── client/                 # Frontend React application
│   ├── src/
│   │   ├── components/     # Reusable UI components
│   │   │   ├── ui/         # Shadcn/ui base components
│   │   │   ├── app-sidebar.tsx
│   │   │   ├── betting-panel.tsx
│   │   │   ├── create-post-form.tsx
│   │   │   ├── market-card.tsx
│   │   │   ├── post-card.tsx
│   │   │   └── theme-toggle.tsx
│   │   ├── pages/          # Route pages
│   │   │   ├── landing.tsx
│   │   │   ├── home.tsx
│   │   │   ├── markets.tsx
│   │   │   ├── create-market.tsx
│   │   │   ├── market-detail.tsx
│   │   │   ├── profile.tsx
│   │   │   ├── groups.tsx
│   │   │   └── leaderboard.tsx
│   │   ├── hooks/          # Custom React hooks
│   │   │   └── useAuth.ts
│   │   └── lib/            # Utilities and helpers
│   │       ├── queryClient.ts
│   │       ├── utils.ts
│   │       └── authUtils.ts
│   └── public/             # Static assets
├── server/                 # Backend Express application
│   ├── routes.ts           # API endpoint definitions
│   ├── storage.ts          # Database operations (IStorage interface)
│   ├── replitAuth.ts       # Authentication middleware
│   └── db.ts               # Database connection
├── shared/                 # Shared code between frontend/backend
│   └── schema.ts           # Drizzle schema & TypeScript types
└── docs/                   # Documentation
```

## Design Patterns

### Frontend Architecture

- **Component-Based**: Reusable UI components in `/components`
- **Page Components**: Route-level components in `/pages`
- **Custom Hooks**: Shared logic extracted to `/hooks`
- **Type Safety**: Full TypeScript with shared schema types

### Backend Architecture

- **Storage Interface**: All database operations go through `IStorage` interface
- **Thin Routes**: API routes delegate to storage layer
- **Validation**: Zod schemas validate all request bodies
- **Session-Based Auth**: Express sessions with wallet verification

### Data Flow

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   React     │────▶│   Express   │────▶│  PostgreSQL │
│   Frontend  │◀────│   Backend   │◀────│   Database  │
└─────────────┘     └─────────────┘     └─────────────┘
       │                   │
       │                   ▼
       │            ┌─────────────┐
       └───────────▶│ DexScreener │
                    │     API     │
                    └─────────────┘
```

## Database Schema

### Core Tables

| Table | Purpose |
|-------|---------|
| `users` | User profiles with stats and wallet addresses |
| `markets` | Prediction markets with targets and status |
| `predictions` | User predictions on markets |
| `bets` | SOL bets placed on markets |
| `posts` | Social feed posts |
| `comments` | Comments on posts |
| `likes` | Post/comment likes |
| `follows` | User follow relationships |
| `groups` | Alpha trading groups |
| `group_members` | Group membership |
| `copied_trades` | Saved/copied trades |

### Key Relationships

- Users create Markets, Predictions, Bets, Posts
- Markets have many Predictions and Bets
- Posts have many Comments and Likes
- Users follow other Users
- Groups have many Members

## Technology Choices

### Why PostgreSQL?
- Complex relational data (users, markets, bets, social)
- ACID transactions for financial operations
- Drizzle ORM for type-safe queries

### Why Solana Wallet Auth?
- Native crypto user experience
- No email/password management
- Cryptographic signature verification

### Why DexScreener?
- Real-time Solana token prices
- Market cap data
- Social links and metadata
