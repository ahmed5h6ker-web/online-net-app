# OnlineNet - Digital Wallet & Internet Subscription Platform

## Overview
OnlineNet is a digital wallet and internet subscription marketplace built with Expo React Native. Users can register, manage wallet balance, browse internet networks, purchase packages, renew hotspot accounts, and submit top-up requests.

## Architecture

### Frontend (Expo React Native)
- **Framework**: Expo SDK 53+ with Expo Router (file-based routing)
- **State Management**: React Context + AsyncStorage for persistence
- **UI**: Custom dark theme (navy/cyan), RTL-friendly, Arabic language

### Backend (Express)
- **Port**: 5000
- **Serves**: Landing page at `/`, API routes at `/api/*`
- **Note**: App data is stored locally via AsyncStorage — backend not required for app functionality

## App Structure
```
app/
  _layout.tsx          # Root layout with all providers
  index.tsx            # Auth redirect
  (auth)/
    _layout.tsx        # Auth stack
    login.tsx          # Phone + password login
    register.tsx       # User registration
  (tabs)/
    _layout.tsx        # Tab bar (NativeTabs iOS 26+, Classic fallback)
    index.tsx          # Home (wallet balance, quick actions, recent transactions)
    networks.tsx       # Available networks list
    transactions.tsx   # Transaction history with filter
    profile.tsx        # User profile, stats, quick actions, logout
  network/
    [id].tsx           # Packages for selected network
  purchase/
    confirm.tsx        # Purchase confirmation + success
  renew/
    index.tsx          # Multi-step renew flow
  topup/
    index.tsx          # Top-up request with amount + image upload

context/
  AuthContext.tsx      # User auth state (AsyncStorage)
  WalletContext.tsx    # Wallet balance + transactions (AsyncStorage)

constants/
  colors.ts            # Dark navy/cyan theme
  mock-data.ts         # Networks and packages data
```

## Design
- **Color Palette**: Deep navy (#050E1A) + cyan accent (#00D4FF)
- **Font**: Inter (400, 500, 600, 700)
- **Language**: Arabic (RTL layout)
- **Theme**: Dark mode primary, light mode supported

## Key Features
1. Phone-based auth (login/register) with AsyncStorage persistence
2. Wallet balance card with gradient design
3. Multi-network support (scalable architecture)
4. Package purchase with commission calculation
5. Multi-step renewal flow
6. Top-up request with optional receipt image
7. Transaction history with type filters
8. Profile with stats and quick actions

## Data Model
- **Users**: id, name, phone, password (hashed in storage), role
- **Networks**: id, name, description, commissionPercentage, status, coverageArea
- **Packages**: id, networkId, name, price, speed, durationDays, mikrotikProfileName
- **Transactions**: id, userId, networkId, type, amount, commission, status, reference
- **TopupRequests**: id, userId, amount, imagePath, status

## Workflows
- **Start Backend**: `npm run server:dev` (port 5000) - serves landing page
- **Start Frontend**: `npm run expo:dev` (port 8081) - Expo Metro bundler
