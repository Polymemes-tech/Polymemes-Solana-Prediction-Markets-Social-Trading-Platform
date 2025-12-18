# Polymemes

**Solana Prediction Markets & Social Trading Platform**

Polymemes is a web-based prediction market and social trading platform built specifically for Solana meme coins and altcoins. Users can create prediction markets by pasting any Solana token contract address, share their trades on a Facebook-style social feed, copy successful traders, join exclusive alpha groups, and compete on accuracy-based leaderboards.

---

## Key Features

### Prediction Markets
- Create markets for any Solana token by pasting the contract address
- Set target conditions: price thresholds or market cap goals
- Define time horizons for predictions to resolve
- Real-time price tracking via DexScreener API integration
- 0.02 SOL market creation fee
- Place real SOL bets with automated payouts on resolution

### Social Trading Feed
- Share trades, predictions, and market commentary
- Facebook-style feed with likes, comments, and engagement
- Copy trades from successful traders with one click
- Track your copied trades in your profile
- Follow your favorite traders for updates

### Copy Trading System
- Save trades from any user to your profile
- View all your copied trades in a dedicated tab
- 2% fee on early position sales
- Learn from top performers and replicate their strategies

### Alpha Groups
- Create public or private trading communities
- Invite-only private groups for exclusive alpha
- Share insights and strategies with group members
- Group chat and discussion features
- Discover trending groups to join

### Leaderboards & Reputation
- Compete based on prediction accuracy
- Build reputation through successful predictions
- Track win rates, total predictions, and streaks
- Discover top performers in the community

### Wallet Integration
- Secure Phantom wallet authentication
- Signature-based verification (no passwords)
- Direct SOL transactions for bets and fees
- View your wallet balance in the app

### Live Market Data
- Real-time price and market cap from DexScreener
- Embedded charts with historical data
- Social links and token metadata
- 30-second auto-refresh for latest prices

---

## Quick Start

```bash
# Clone the repository
git clone https://github.com/your-username/polymemes.git
cd polymemes

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your database URL and secrets

# Push database schema
npm run db:push

# Start development server
npm run dev
```

The application runs on `http://localhost:5000`

---

## Tech Stack

### Frontend
| Technology | Purpose |
|------------|---------|
| React 18 | UI framework with hooks |
| TypeScript | Type-safe development |
| Vite | Fast build tool and dev server |
| TailwindCSS | Utility-first styling |
| Shadcn/ui | Pre-built UI components |
| TanStack Query | Data fetching and caching |
| Wouter | Lightweight routing |
| Framer Motion | Smooth animations |

### Backend
| Technology | Purpose |
|------------|---------|
| Express.js | HTTP server and API |
| Node.js | JavaScript runtime |
| PostgreSQL | Relational database |
| Drizzle ORM | Type-safe database queries |
| express-session | Session management |

### Blockchain & Crypto
| Technology | Purpose |
|------------|---------|
| @solana/web3.js | Solana blockchain interaction |
| tweetnacl | Cryptographic signatures |
| bs58 | Base58 encoding for addresses |
| Phantom Wallet | User authentication |

### External APIs
| Service | Purpose |
|---------|---------|
| DexScreener | Real-time token prices and charts |

---

## Project Structure

```
polymemes/
├── client/                    # Frontend React application
│   └── src/
│       ├── components/        # Reusable UI components
│       │   ├── ui/            # Shadcn base components
│       │   ├── app-sidebar.tsx
│       │   ├── post-card.tsx
│       │   ├── market-card.tsx
│       │   └── wallet-button.tsx
│       ├── pages/             # Route pages
│       │   ├── landing.tsx    # Public landing page
│       │   ├── home.tsx       # Main feed (authenticated)
│       │   ├── markets.tsx    # Markets listing
│       │   ├── create-market.tsx
│       │   ├── market-detail.tsx
│       │   ├── profile.tsx
│       │   ├── groups.tsx
│       │   └── leaderboard.tsx
│       ├── hooks/             # Custom React hooks
│       │   └── useAuth.ts
│       └── lib/               # Utilities
│           ├── queryClient.ts
│           └── authUtils.ts
├── server/                    # Backend Express application
│   ├── routes.ts              # API endpoint definitions
│   ├── storage.ts             # Database operations
│   ├── db.ts                  # Database connection
│   └── replitAuth.ts          # Authentication middleware
├── shared/                    # Shared code
│   └── schema.ts              # Database schema & TypeScript types
├── docs/                      # Extended documentation
│   ├── ARCHITECTURE.md
│   ├── API.md
│   ├── AUTHENTICATION.md
│   └── FEATURES.md
└── design_guidelines.md       # UI/UX design system
```

---

## Database Schema

### Core Tables

| Table | Description |
|-------|-------------|
| `users` | User profiles with wallet addresses, stats, and reputation |
| `markets` | Prediction markets with target conditions and deadlines |
| `predictions` | User bets on market outcomes |
| `posts` | Social feed content (trades, predictions, commentary) |
| `comments` | Comments on posts |
| `likes` | Post and comment likes |
| `follows` | User follow relationships |
| `groups` | Alpha trading groups (public/private) |
| `group_members` | Group membership records |
| `copied_trades` | Saved/copied trades from other users |
| `sessions` | User authentication sessions |

---

## API Endpoints

### Authentication
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/wallet/nonce` | Request nonce for wallet signature |
| POST | `/api/auth/wallet` | Authenticate with signed message |
| POST | `/api/auth/logout` | End user session |
| GET | `/api/auth/user` | Get current authenticated user |

### Markets
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/markets` | List all markets |
| POST | `/api/markets` | Create new market |
| GET | `/api/markets/:id` | Get market details |
| POST | `/api/markets/:id/predict` | Place prediction bet |

### Social
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/posts` | List feed posts |
| POST | `/api/posts` | Create new post |
| POST | `/api/posts/:id/like` | Toggle like on post |
| POST | `/api/posts/:id/copy` | Copy/save trade |
| DELETE | `/api/posts/:id` | Delete own post |

### Users
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/users/:id` | Get user profile |
| GET | `/api/users/:id/posts` | Get user's posts |
| GET | `/api/users/:id/markets` | Get user's markets |
| GET | `/api/users/:id/bets` | Get user's predictions |
| GET | `/api/users/:id/copied-trades` | Get user's copied trades |
| POST | `/api/users/:id/follow` | Toggle follow user |

### Groups
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/groups` | List all groups |
| POST | `/api/groups` | Create new group |
| POST | `/api/groups/:id/join` | Join or leave group |

### Data
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/tokens/:address` | Fetch token data from DexScreener |
| GET | `/api/leaderboard` | Get top traders leaderboard |
| GET | `/api/stats` | Get platform statistics |

---

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `DATABASE_URL` | Yes | PostgreSQL connection string |
| `SESSION_SECRET` | Yes | Secret for Express sessions |
| `WALLET_ENCRYPTION_KEY` | Yes | Encryption key for wallet data |
| `NODE_ENV` | No | Environment (development/production) |

---

## Design System

Polymemes uses a dark crypto trading terminal aesthetic:

- **Primary Color**: Mint green (#7dd3a8) for success states and accents
- **Background**: Dark charcoal (#1e2530) with subtle gradients
- **Typography**: Inter for UI, JetBrains Mono for prices and data
- **Effects**: Glassmorphism cards, smooth animations, subtle glows
- **Theme**: Dark mode by default with optional light mode

---

## Documentation

For detailed documentation, see the `/docs` folder:

- **[Architecture & Project Structure](docs/ARCHITECTURE.md)** - Technical architecture, folder structure, and design decisions
- **[API Reference](docs/API.md)** - Complete API documentation with request/response examples
- **[Authentication System](docs/AUTHENTICATION.md)** - Wallet-based auth flow and session management
- **[Features Guide](docs/FEATURES.md)** - Detailed feature descriptions and user flows

---

## Development

### Running Locally

```bash
# Development mode with hot reload
npm run dev

# Database commands
npm run db:push      # Push schema changes
npm run db:studio    # Open Drizzle Studio GUI
```

### Code Style

- TypeScript strict mode enabled
- ESLint for code linting
- Prettier for code formatting
- Component-based architecture
- Shared types between frontend and backend

---

## Contributing

Contributions are welcome! Before submitting a pull request:

1. Read the documentation in `/docs`
2. Follow the existing code style
3. Test your changes thoroughly
4. Update documentation if needed

---

## Support

If you encounter issues or have questions:

1. Check the documentation in `/docs`
2. Search existing issues
3. Open a new issue with detailed information

---

Built with Solana, React, and community-driven development.
