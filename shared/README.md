# ChargeX Shared Libraries & Utilities

## 📦 Overview

Shared code, libraries, and utilities used across the ChargeX platform components. This ensures consistency and reduces code duplication between the main website, application, and hardware components.

## 🏗️ Structure

```
shared/
├── types/              # TypeScript type definitions
│   ├── battery.ts      # Battery-related types
│   ├── user.ts         # User profile types
│   ├── trading.ts      # Energy trading types
│   └── telemetry.ts    # IoT data types
├── constants/          # Application constants
│   ├── config.ts       # Configuration constants
│   ├── endpoints.ts    # API endpoints
│   └── tokens.ts       # Token addresses & configs
├── utils/              # Utility functions
│   ├── validation.ts   # Data validation helpers
│   ├── formatting.ts   # Data formatting utilities
│   ├── crypto.ts       # Cryptographic functions
│   └── datetime.ts     # Date/time utilities
├── hooks/              # Shared React hooks
│   ├── useICP.ts       # ICP integration hook
│   ├── useBattery.ts   # Battery data hook
│   └── useTrading.ts   # Trading functionality hook
├── components/         # Reusable UI components
│   ├── Button/         # Custom button component
│   ├── Modal/          # Modal component
│   ├── Chart/          # Chart components
│   └── Form/           # Form components
└── services/           # Shared service modules
    ├── icp.ts          # ICP SDK wrapper
    ├── api.ts          # API client
    └── storage.ts      # Local storage utilities
```

## 🎯 Key Modules

### Type Definitions
- **Battery Types**: BatteryStatus, BatteryLease, BatteryHealth
- **User Types**: UserProfile, UserPreferences, UserActivity
- **Trading Types**: EnergyOffer, TradeTransaction, MarketData
- **Telemetry Types**: SensorData, LocationData, AlertData

### Utility Functions
- **Validation**: Input validation, schema validation
- **Formatting**: Currency, date, battery metrics
- **Crypto**: Hashing, encryption, signature verification
- **DateTime**: Timezone handling, formatting, calculations

### React Hooks
- **useICP**: ICP connection, authentication, canister calls
- **useBattery**: Battery data fetching, real-time updates
- **useTrading**: Market data, trading operations

### UI Components
- **Consistent Styling**: Shared design system
- **Accessibility**: WCAG compliant components
- **Responsive Design**: Mobile-first approach
- **Theme Support**: Light/dark mode

## 🛠️ Development

### Installation
```bash
cd shared
npm install
```

### Building
```bash
# Build TypeScript
npm run build

# Watch mode for development
npm run dev

# Type checking
npm run type-check
```

### Testing
```bash
# Run unit tests
npm test

# Coverage report
npm run test:coverage

# Integration tests
npm run test:integration
```

## 📋 Usage Examples

### Type Definitions
```typescript
import { BatteryStatus, UserProfile } from '@chargex/shared/types';

const battery: BatteryStatus = {
  id: 'bat_123',
  voltage: 12.6,
  current: 2.5,
  temperature: 25.0,
  location: { lat: 40.7128, lng: -74.0060 },
  health: 'good'
};
```

### Utility Functions
```typescript
import { formatCurrency, validateBatteryData } from '@chargex/shared/utils';

const price = formatCurrency(25.50, 'USD');
const isValid = validateBatteryData(batteryData);
```

### React Hooks
```typescript
import { useICP, useBattery } from '@chargex/shared/hooks';

function BatteryDashboard() {
  const { isAuthenticated, login } = useICP();
  const { batteries, loading } = useBattery();
  
  return (
    <div>
      {loading ? 'Loading...' : batteries.map(battery => ...)}
    </div>
  );
}
```

## 🔄 Versioning

- **Semantic Versioning**: Major.Minor.Patch
- **Breaking Changes**: Major version bump
- **New Features**: Minor version bump
- **Bug Fixes**: Patch version bump

## 📦 Publishing

```bash
# Build for production
npm run build

# Publish to npm (if public)
npm publish

# Link for local development
npm link
```

## 🧪 Quality Assurance

- **ESLint**: Code linting and formatting
- **Prettier**: Code formatting
- **TypeScript**: Static type checking
- **Jest**: Unit testing framework
- **Husky**: Git hooks for quality gates
