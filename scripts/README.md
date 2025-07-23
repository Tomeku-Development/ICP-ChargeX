# ChargeX Scripts & Utilities

## 🛠️ Overview

Build automation, utility scripts, and development tools for the ChargeX platform. These scripts streamline development, testing, and deployment processes.

## 🏗️ Structure

```
scripts/
├── build/              # Build automation
│   ├── build-all.sh    # Build entire platform
│   ├── build-canisters.sh  # Build ICP canisters
│   ├── build-frontend.sh   # Build React frontend
│   └── build-hardware.sh   # Compile hardware code
├── deploy/             # Deployment scripts
│   ├── deploy-local.sh     # Local deployment
│   ├── deploy-staging.sh   # Staging deployment
│   └── deploy-production.sh # Production deployment
├── test/               # Testing automation
│   ├── run-tests.sh    # Run all tests
│   ├── integration-tests.sh # Integration testing
│   └── e2e-tests.sh    # End-to-end testing
├── setup/              # Environment setup
│   ├── setup-dev.sh    # Development environment
│   ├── install-deps.sh # Install dependencies
│   └── configure-env.sh # Environment configuration
└── utils/              # Utility scripts
    ├── clean.sh        # Clean build artifacts
    ├── lint.sh         # Code linting
    └── format.sh       # Code formatting
```

## 🎯 Key Scripts

### Build Scripts
- **build-all.sh**: Complete platform build
- **build-canisters.sh**: ICP canister compilation
- **build-frontend.sh**: React app build
- **build-hardware.sh**: ESP32/Arduino compilation

### Deployment Scripts
- **deploy-local.sh**: Local replica deployment
- **deploy-staging.sh**: Staging environment deployment
- **deploy-production.sh**: Production deployment with safety checks

### Testing Scripts  
- **run-tests.sh**: Comprehensive test suite
- **integration-tests.sh**: Cross-component testing
- **e2e-tests.sh**: End-to-end user journey tests

### Setup Scripts
- **setup-dev.sh**: One-command development setup
- **install-deps.sh**: Install all project dependencies
- **configure-env.sh**: Environment configuration

## 🚀 Usage Examples

```bash
# Quick development setup
./scripts/setup/setup-dev.sh

# Build entire platform
./scripts/build/build-all.sh

# Run all tests
./scripts/test/run-tests.sh

# Deploy to local replica
./scripts/deploy/deploy-local.sh

# Clean build artifacts
./scripts/utils/clean.sh
```
