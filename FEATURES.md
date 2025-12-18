# Features Guide

## Prediction Markets

### Creating a Market

1. Navigate to **Create Market** page
2. Paste a Solana token contract address
3. Token data auto-fetches from DexScreener
4. Set your prediction parameters:
   - **Target Type**: Price or Market Cap
   - **Direction**: Above or Below target
   - **Target Value**: Your predicted threshold
   - **End Date**: When the market resolves
5. Pay 0.02 SOL creation fee
6. Market goes live immediately

### Market Resolution

Markets resolve automatically when:
- Target is reached before end date → **Resolved YES**
- End date passes without reaching target → **Resolved NO**
- Manual resolution by creator (edge cases)

### Betting on Markets

1. Open any active market
2. Choose **YES** or **NO** position
3. Enter SOL amount to bet
4. Confirm transaction in wallet
5. Track your position in the market

### Odds & Payouts

- Odds determined by bet pool ratios
- Displayed as percentages (e.g., 65% YES / 35% NO)
- Winners split the losing pool proportionally
- 2% platform fee on winnings

### Selling Positions Early

- Sell your position before market resolves
- 2% exit fee applies
- Payout based on current odds
- Instant settlement to wallet

---

## Social Feed

### Post Types

| Type | Description |
|------|-------------|
| **Trade** | Share a trade you made with entry/exit details |
| **Prediction** | Share your market prediction with reasoning |
| **General** | Discussion, alpha, or commentary |

### Creating Posts

1. Click **Create Post** in feed
2. Select post type
3. Write your content
4. Optionally attach a market reference
5. Add images if desired
6. Post to feed

### Engagement

- **Like**: Show appreciation for posts
- **Comment**: Add your thoughts
- **Copy Trade**: Save trades to your watchlist
- **Share**: Link to the post

---

## Copy Trading

### How It Works

1. Browse the feed or leaderboard
2. Find traders with good track records
3. Click **Copy** on their trade posts
4. Trade appears in your Copied Trades
5. Get notifications on their future trades

### Tracking Copied Trades

- View all copied trades in Profile
- See original trader performance
- Compare to your own execution
- Unfollow trades anytime

---

## Alpha Groups

### Group Types

| Type | Description |
|------|-------------|
| **Public** | Anyone can join and view content |
| **Private** | Invite-only, hidden content |

### Creating a Group

1. Go to **Groups** page
2. Click **Create Group**
3. Set name and description
4. Choose public or private
5. Invite members (if private)

### Group Features

- Dedicated feed for group posts
- Member leaderboard
- Group statistics
- Admin controls for private groups

### Joining Groups

- **Public**: Click Join button
- **Private**: Request invite or use invite link

---

## Leaderboards

### Ranking Metrics

| Metric | Description |
|--------|-------------|
| **Accuracy** | % of correct predictions |
| **Total Predictions** | Number of markets predicted |
| **Reputation** | Combined score from all activity |
| **Profit** | Total SOL profit from bets |

### Time Periods

- **All Time**: Complete history
- **Monthly**: Current month only
- **Weekly**: Last 7 days

### Badges & Achievements

Earn badges for:
- Top 10 weekly accuracy
- 100+ predictions milestone
- 10 winning streak
- Community contributor

---

## User Profile

### Profile Components

- **Avatar**: Upload custom image
- **Username**: Editable display name
- **Bio**: Short description
- **Stats**: Predictions, accuracy, followers
- **Activity**: Recent posts and predictions

### Stats Tracked

| Stat | Description |
|------|-------------|
| Predictions | Total predictions made |
| Accuracy | % of correct predictions |
| Reputation | Community standing score |
| Followers | Users following you |
| Following | Users you follow |

### Privacy

- Wallet address shortened in UI
- Full address visible on profile
- Trade history is public
- DMs not currently supported

---

## Live Data

### DexScreener Integration

Real-time data for all tokens:
- Current price (USD)
- Market cap
- 24h price change
- 24h volume
- Liquidity depth

### Embedded Charts

- Interactive TradingView-style charts
- Multiple timeframes (1m to 1M)
- Volume overlay
- Powered by DexScreener widgets

### Data Refresh

- Market detail: Every 30 seconds
- Market list: On page load
- Feed: Real-time updates

---

## Wallet Integration

### Supported Wallets

- **Phantom** (recommended)

### Transactions

All on-chain transactions:
1. Market creation fee (0.02 SOL)
2. Placing bets (variable SOL)
3. Claiming winnings
4. Selling positions

### Transaction Flow

1. Action triggers transaction request
2. Wallet popup shows details
3. User confirms in wallet
4. Transaction submitted to Solana
5. Confirmation received
6. UI updates automatically

### Gas Fees

- Standard Solana transaction fees apply
- Typically < 0.001 SOL per transaction
- Shown in wallet before confirmation
