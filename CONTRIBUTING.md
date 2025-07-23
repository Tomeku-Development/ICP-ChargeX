# Contributing to ChargeX

We love your input! We want to make contributing to ChargeX as easy and transparent as possible, whether it's:

- Reporting a bug
- Discussing the current state of the code
- Submitting a fix
- Proposing new features
- Becoming a maintainer

## 🚀 Development Process

We use GitHub to host code, to track issues and feature requests, as well as accept pull requests.

### Pull Requests
1. Fork the repo and create your branch from `main`
2. If you've added code that should be tested, add tests
3. If you've changed APIs, update the documentation
4. Ensure the test suite passes
5. Make sure your code lints
6. Issue that pull request!

### Development Setup
```bash
# Fork and clone the repository
git clone https://github.com/YOUR_USERNAME/ICP-ChargeX.git
cd ICP-ChargeX

# Install dependencies
npm run setup

# Start development environment
dfx start --background
dfx deploy
npm run dev
```

## 📝 Code Style

- Use meaningful variable and function names
- Write clear, concise comments
- Follow Rust conventions for canister code
- Follow React/TypeScript best practices for frontend
- Use ESLint and Prettier for code formatting

### Commit Messages
- Use the present tense ("Add feature" not "Added feature")
- Use the imperative mood ("Move cursor to..." not "Moves cursor to...")
- Limit the first line to 72 characters or less
- Reference issues and pull requests liberally after the first line

## 🐛 Bug Reports

**Great Bug Reports** tend to have:

- A quick summary and/or background
- Steps to reproduce
  - Be specific!
  - Give sample code if you can
- What you expected would happen
- What actually happens
- Notes (possibly including why you think this might be happening, or stuff you tried that didn't work)

## 💡 Feature Requests

We track feature requests as GitHub issues. When creating a feature request:

- Use a clear and descriptive title
- Provide a step-by-step description of the suggested enhancement
- Explain why this enhancement would be useful
- List some other applications where this enhancement exists

## 🏗️ Project Areas

### Frontend (React.js)
- Battery leasing interface
- Energy trading marketplace
- Real-time dashboard
- Mobile responsiveness

### Backend (ICP Canisters)
- Leasing & Trading logic
- Telemetry data processing
- AI inference models
- User profile management

### Hardware (IoT)
- ESP32 firmware
- Sensor integration
- Raspberry Pi kiosk
- Hardware-software communication

### Documentation
- Technical documentation
- User guides
- API documentation
- Architecture diagrams

## 📄 License

By contributing, you agree that your contributions will be licensed under the MIT License.

## 🤝 Code of Conduct

This project and everyone participating in it is governed by our Code of Conduct. By participating, you are expected to uphold this code.

## ❓ Questions?

Feel free to reach out:
- Open an issue for bugs or feature requests
- Join our [Discord](https://discord.gg/chargex)
- Email us at dev@chargex.io
