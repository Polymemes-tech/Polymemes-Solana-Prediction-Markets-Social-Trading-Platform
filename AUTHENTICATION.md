# Authentication System

## Overview

Polymemes uses Solana wallet-based authentication. Users sign a message with their Phantom wallet to prove ownership of their wallet address.

## Authentication Flow

```
┌──────────┐     ┌──────────┐     ┌──────────┐
│  Client  │     │  Server  │     │  Wallet  │
└────┬─────┘     └────┬─────┘     └────┬─────┘
     │                │                │
     │  1. Request    │                │
     │    Nonce       │                │
     │───────────────▶│                │
     │                │                │
     │  2. Return     │                │
     │    Nonce       │                │
     │◀───────────────│                │
     │                │                │
     │  3. Sign Message               │
     │───────────────────────────────▶│
     │                │                │
     │  4. Return Signature           │
     │◀───────────────────────────────│
     │                │                │
     │  5. Submit     │                │
     │    Signature   │                │
     │───────────────▶│                │
     │                │  6. Verify     │
     │                │    Signature   │
     │                │                │
     │  7. Session    │                │
     │    Created     │                │
     │◀───────────────│                │
```

## Step-by-Step

### 1. Request Nonce

Client requests a unique nonce for the wallet address:

```typescript
const response = await fetch('/api/auth/wallet/nonce', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ walletAddress })
});

const { nonce, message } = await response.json();
```

### 2. Sign Message

User signs the message with Phantom wallet:

```typescript
const encodedMessage = new TextEncoder().encode(message);
const signedMessage = await window.solana.signMessage(encodedMessage, 'utf8');
const signature = bs58.encode(signedMessage.signature);
```

### 3. Verify & Authenticate

Submit signature for verification:

```typescript
const response = await fetch('/api/auth/wallet', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    walletAddress,
    signature,
    nonce
  })
});

const user = await response.json();
```

## Server-Side Verification

The server verifies the signature using `tweetnacl`:

```typescript
import nacl from 'tweetnacl';
import bs58 from 'bs58';

function verifySignature(
  message: string,
  signature: string,
  publicKey: string
): boolean {
  const messageBytes = new TextEncoder().encode(message);
  const signatureBytes = bs58.decode(signature);
  const publicKeyBytes = bs58.decode(publicKey);
  
  return nacl.sign.detached.verify(
    messageBytes,
    signatureBytes,
    publicKeyBytes
  );
}
```

## Session Management

- Sessions stored server-side using `express-session`
- Session cookie sent with each request
- Sessions persist across page refreshes
- Logout destroys session

## Security Considerations

### Nonce Security
- Nonces are single-use and expire after 5 minutes
- Prevents replay attacks
- Tied to specific wallet address

### Signature Security
- Uses Ed25519 cryptographic signatures
- Message contains human-readable context
- Wallet address extracted from public key

### Session Security
- HTTP-only cookies prevent XSS
- Secure flag enabled in production
- Sessions stored in PostgreSQL

## Frontend Hook

The `useAuth` hook manages authentication state:

```typescript
import { useAuth } from '@/hooks/useAuth';

function Component() {
  const { user, isLoading, login, logout } = useAuth();
  
  if (isLoading) return <Spinner />;
  
  if (!user) {
    return <Button onClick={login}>Connect Wallet</Button>;
  }
  
  return (
    <div>
      <span>{user.username}</span>
      <Button onClick={logout}>Disconnect</Button>
    </div>
  );
}
```

## Wallet Support

Currently supported:
- **Phantom** - Primary wallet

The authentication system is designed to support additional Solana wallets that implement the standard wallet adapter interface.

## User Creation

When a new wallet authenticates:
1. Check if user exists with wallet address
2. If not, create new user with:
   - Auto-generated username from wallet address
   - Default profile settings
   - Initial stats (0 predictions, 0 accuracy)

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Invalid signature | Wrong wallet or tampered message | Re-sign with correct wallet |
| Nonce expired | Took too long to sign | Request new nonce |
| Wallet not connected | Phantom not installed/locked | Connect Phantom first |
