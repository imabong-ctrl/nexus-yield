# Nexus Yield

[![Clarity](https://img.shields.io/badge/Clarity-v3-brightgreen)](https://docs.stacks.co/clarity/)
[![Stacks](https://img.shields.io/badge/Stacks-Bitcoin--secured-orange)](https://www.stacks.co/)
[![License](https://img.shields.io/badge/License-ISC-blue.svg)](LICENSE)

> **Enterprise-grade Bitcoin-backed lending protocol on Stacks blockchain**

Nexus Yield is a sophisticated decentralized lending protocol that enables Bitcoin holders to access liquidity without sacrificing their BTC position. Built with advanced risk management features including dynamic collateralization ratios, automated liquidation protection, and real-time price feeds.

## 🌟 Features

### Core Functionality

- **🔒 Bitcoin Collateralization**: Secure your loans with Bitcoin holdings
- **💰 Stablecoin Lending**: Access liquidity through collateralized loans
- **⚡ Real-time Price Feeds**: Dynamic pricing through oracle integration
- **🛡️ Automated Risk Management**: Intelligent liquidation protection
- **📊 Multi-asset Support**: Extensible infrastructure for multiple collateral types

### Risk Management

- **Dynamic Collateralization**: Configurable collateral ratios (default: 150%)
- **Liquidation Protection**: Automated position monitoring and protection
- **Interest Rate Models**: Flexible and competitive interest calculations
- **Capital Efficiency**: Optimized collateral utilization

## 🏗️ Architecture

### Smart Contract Structure

```text
nexus-yield.clar
├── Platform Management
├── Lending Operations
├── Risk Management
├── Governance Functions
└── Read-Only Queries
```

### Key Components

- **Loan Management**: Complete loan lifecycle management
- **Collateral Tracking**: Real-time collateral monitoring
- **Price Oracle Integration**: External price feed support
- **User Portfolio Management**: Multi-loan user interface
- **Liquidation Engine**: Automated risk mitigation

## 🚀 Quick Start

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) v2.0+
- [Node.js](https://nodejs.org/) v18+
- [Stacks CLI](https://docs.stacks.co/stacks-cli) (optional)

### Installation

```bash
# Clone the repository
git clone https://github.com/imabong-ctrl/nexus-yield.git
cd nexus-yield

# Install dependencies
npm install

# Initialize Clarinet
clarinet check
```

### Testing

```bash
# Run all tests
npm test

# Run tests with coverage and cost analysis
npm run test:report

# Watch mode for development
npm run test:watch

# Clarinet specific tests
clarinet test
```

### Deployment

```bash
# Check contracts
clarinet check

# Deploy to devnet
clarinet integrate

# Deploy to testnet (requires configuration)
clarinet deploy --testnet

# Deploy to mainnet (requires configuration)
clarinet deploy --mainnet
```

## 📖 Usage

### Platform Initialization

```clarity
;; Initialize the platform (owner only)
(contract-call? .nexus-yield initialize-platform)
```

### Creating a Loan

```clarity
;; 1. Deposit collateral
(contract-call? .nexus-yield deposit-collateral u1000000) ;; 1 BTC in sats

;; 2. Request loan
(contract-call? .nexus-yield request-loan u1000000 u50000000) ;; Collateral and loan amount
```

### Managing Loans

```clarity
;; Repay a loan
(contract-call? .nexus-yield repay-loan u1 u50000000) ;; Loan ID and amount

;; Check loan details
(contract-call? .nexus-yield get-loan-details u1)

;; View user's active loans
(contract-call? .nexus-yield get-user-loans tx-sender)
```

### Price Feed Management

```clarity
;; Update BTC price (owner only)
(contract-call? .nexus-yield update-price-feed "BTC" u6500000) ;; $65,000 USD

;; Update collateral ratio (owner only)
(contract-call? .nexus-yield update-collateral-ratio u160) ;; 160%
```

## 🔧 Configuration

### Environment Files

- `settings/Devnet.toml` - Local development configuration
- `settings/Testnet.toml` - Testnet deployment settings
- `settings/Mainnet.toml` - Production deployment settings

### Key Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| Minimum Collateral Ratio | 150% | Required overcollateralization |
| Liquidation Threshold | 120% | Triggers automatic liquidation |
| Platform Fee Rate | 1% | Protocol fee on loans |
| Interest Rate | 5% | Default annual interest rate |

## 📊 Risk Management

### Collateralization Model

- **Initial Collateral**: 150% minimum ratio
- **Liquidation Trigger**: 120% ratio
- **Safety Buffer**: 30% protection margin

### Liquidation Process

1. **Monitoring**: Real-time ratio calculation
2. **Threshold Check**: Automated position analysis
3. **Liquidation**: Automatic collateral seizure
4. **Settlement**: Position closure and cleanup

### Price Feed Security

- **Oracle Integration**: External price feed support
- **Price Validation**: Range and sanity checks
- **Fallback Mechanisms**: Emergency price handling

## 🛠️ Development

### Project Structure

```text
nexus-yield/
├── contracts/
│   └── nexus-yield.clar      # Main contract
├── tests/
│   └── nexus-yield.test.ts   # Test suite
├── settings/
│   ├── Devnet.toml          # Dev configuration
│   ├── Testnet.toml         # Test configuration
│   └── Mainnet.toml         # Prod configuration
├── Clarinet.toml            # Project configuration
├── package.json             # Node dependencies
└── vitest.config.js         # Test configuration
```

### Adding Features

1. **Contract Modifications**: Edit `contracts/nexus-yield.clar`
2. **Test Coverage**: Update `tests/nexus-yield.test.ts`
3. **Validation**: Run `clarinet check` and `npm test`
4. **Documentation**: Update relevant sections

### Code Style

- Follow [Clarity coding standards](https://book.clarity-lang.org/ch02-01-syntax.html)
- Use descriptive function and variable names
- Include comprehensive error handling
- Add inline documentation for complex logic

## 🔍 API Reference

### Public Functions

#### Platform Management

- `initialize-platform()` - Initialize the lending platform
- `deposit-collateral(amount)` - Deposit BTC collateral

#### Lending Operations

- `request-loan(collateral, loan-amount)` - Create new loan
- `repay-loan(loan-id, amount)` - Repay existing loan

#### Governance

- `update-collateral-ratio(new-ratio)` - Modify collateral requirements
- `update-liquidation-threshold(new-threshold)` - Adjust liquidation trigger
- `update-price-feed(asset, new-price)` - Update asset prices

### Read-Only Functions

- `get-loan-details(loan-id)` - Retrieve loan information
- `get-user-loans(user)` - Get user's active loans
- `get-platform-stats()` - Platform metrics and statistics
- `get-valid-assets()` - List supported assets

### Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| 100 | ERR-NOT-AUTHORIZED | Unauthorized access attempt |
| 101 | ERR-INSUFFICIENT-COLLATERAL | Insufficient collateral provided |
| 102 | ERR-BELOW-MINIMUM | Amount below minimum threshold |
| 103 | ERR-INVALID-AMOUNT | Invalid amount specified |
| 104 | ERR-ALREADY-INITIALIZED | Platform already initialized |
| 105 | ERR-NOT-INITIALIZED | Platform not yet initialized |
| 106 | ERR-INVALID-LIQUIDATION | Invalid liquidation attempt |
| 107 | ERR-LOAN-NOT-FOUND | Loan does not exist |
| 108 | ERR-LOAN-NOT-ACTIVE | Loan is not active |
| 109 | ERR-INVALID-LOAN-ID | Invalid loan identifier |
| 110 | ERR-INVALID-PRICE | Invalid price value |
| 111 | ERR-INVALID-ASSET | Asset not supported |

## 🔐 Security

### Audit Status

- [ ] Internal security review
- [ ] External audit (pending)
- [ ] Formal verification (planned)

### Security Features

- **Access Control**: Owner-only administrative functions
- **Input Validation**: Comprehensive parameter checking
- **Overflow Protection**: Safe arithmetic operations
- **State Consistency**: Atomic state transitions

### Best Practices

- Always validate inputs before processing
- Use read-only functions for data queries
- Implement proper error handling
- Follow principle of least privilege

## 📈 Monitoring

### Key Metrics

- Total BTC Locked
- Active Loans Count
- Average Collateralization Ratio
- Liquidation Events
- Platform Revenue

### Health Indicators

- Price Feed Freshness
- System Collateral Ratio
- User Activity Levels
- Error Rate Monitoring

## 🤝 Contributing

We welcome contributions to Nexus Yield! Please follow these guidelines:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Test** your changes thoroughly
4. **Commit** your changes (`git commit -m 'Add amazing feature'`)
5. **Push** to the branch (`git push origin feature/amazing-feature`)
6. **Open** a Pull Request

### Development Guidelines

- Write comprehensive tests for new features
- Follow existing code style and conventions
- Update documentation for API changes
- Ensure all tests pass before submitting

## 📄 License

This project is licensed under the ISC License - see the [LICENSE](LICENSE) file for details.
