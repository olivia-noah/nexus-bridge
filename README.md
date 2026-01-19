# NexusBridge - Cross-Chain Bitcoin Gateway

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![Clarity](https://img.shields.io/badge/clarity-v3-orange.svg)
![License](https://img.shields.io/badge/license-ISC-green.svg)
![Tests](https://img.shields.io/badge/tests-passing-brightgreen.svg)

## 🌉 Overview

NexusBridge revolutionizes Bitcoin interoperability by creating a decentralized gateway that seamlessly connects Bitcoin with the Stacks ecosystem. This contract establishes a trustless infrastructure for cross-chain value transfer, enabling Bitcoin holders to participate in DeFi applications while maintaining full custody control over their assets.

## ✨ Key Features

- **🔐 Multi-Signature Validation**: Sophisticated consensus mechanism with cryptographic proof verification
- **⚡ Real-Time Monitoring**: Bitcoin transaction monitoring with configurable confirmation thresholds
- **🛡️ Emergency Controls**: Circuit breakers and administrative controls for maximum security
- **⚙️ Gas Optimization**: Efficient operations for high-volume cross-chain transactions
- **📋 Audit Trail**: Comprehensive immutable transaction records
- **💰 Custody Control**: Users maintain full control over their Bitcoin assets

## 🏗️ Architecture

The NexusBridge protocol implements a multi-layered security architecture:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Bitcoin       │    │   NexusBridge   │    │   Stacks DeFi   │
│   Network       │◄──►│   Protocol      │◄──►│   Ecosystem     │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

### Core Components

1. **Validator Network**: Decentralized validators ensure transaction integrity
2. **Deposit Processing**: Secure handling of Bitcoin deposits with confirmation tracking
3. **Consensus Mechanism**: Multi-signature validation for deposit confirmations
4. **Balance Management**: Efficient tracking of bridged assets
5. **Emergency System**: Administrative controls for critical situations

## 🚀 Getting Started

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) v2.0+
- [Node.js](https://nodejs.org/) v18+
- [Stacks CLI](https://docs.stacks.co/stacks-cli)

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/makun-creator/nexus-bridge.git
   cd nexus-bridge
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Run tests**

   ```bash
   npm test
   ```

4. **Check contract syntax**

   ```bash
   clarinet check
   ```

### Project Structure

```
nexus-bridge/
├── contracts/
│   └── nexus-bridge.clar      # Main bridge contract
├── tests/
│   └── nexus-bridge.test.ts   # Contract tests
├── settings/
│   ├── Devnet.toml           # Development network config
│   ├── Testnet.toml          # Testnet configuration
│   └── Mainnet.toml          # Mainnet configuration
├── Clarinet.toml             # Clarinet project config
├── package.json              # Node.js dependencies
└── tsconfig.json             # TypeScript configuration
```

## 📖 Usage

### Core Operations

#### Initialize Bridge

```clarity
(contract-call? .nexus-bridge initialize-bridge)
```

#### Add Validator

```clarity
(contract-call? .nexus-bridge add-validator 'SP2J6ZY48GV1EZ5V2V5RB9MP66SW86PYKKNRV9EJ7)
```

#### Initiate Deposit

```clarity
(contract-call? .nexus-bridge initiate-deposit
  0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef  ;; tx-hash
  u1000000                                                            ;; amount (satoshis)
  'SP2J6ZY48GV1EZ5V2V5RB9MP66SW86PYKKNRV9EJ7                          ;; recipient
  0x03abc123def456789012345678901234567890123456789012345678901234567890  ;; btc-sender
)
```

#### Confirm Deposit

```clarity
(contract-call? .nexus-bridge confirm-deposit
  0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef  ;; tx-hash
  0x3045022100...                                                    ;; validator signature
)
```

#### Withdraw to Bitcoin

```clarity
(contract-call? .nexus-bridge withdraw
  u500000                                                            ;; amount
  0x1234567890abcdef1234567890abcdef12345678                         ;; btc-recipient
)
```

### Read-Only Functions

#### Check Balance

```clarity
(contract-call? .nexus-bridge get-balance 'SP2J6ZY48GV1EZ5V2V5RB9MP66SW86PYKKNRV9EJ7)
```

#### Get Deposit Info

```clarity
(contract-call? .nexus-bridge get-deposit 
  0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef)
```

#### Check Bridge Status

```clarity
(contract-call? .nexus-bridge get-bridge-status)
```

## 🔧 Configuration

### Network Settings

The bridge supports different configurations for various networks:

- **Devnet**: Development and testing environment
- **Testnet**: Public testing network
- **Mainnet**: Production environment

### Security Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| `MIN-DEPOSIT-AMOUNT` | 100,000 satoshis | Minimum deposit (0.001 BTC) |
| `MAX-DEPOSIT-AMOUNT` | 1,000,000,000 satoshis | Maximum deposit (10 BTC) |
| `REQUIRED-CONFIRMATIONS` | 6 blocks | Bitcoin confirmations required |

## 🧪 Testing

The project includes comprehensive test suites:

```bash
# Run all tests
npm test

# Run tests with coverage
npm run test:report

# Watch mode for development
npm run test:watch
```

### Test Categories

- **Unit Tests**: Individual function testing
- **Integration Tests**: Cross-function interactions
- **Security Tests**: Validation of security constraints
- **Edge Cases**: Boundary condition testing

## 🛡️ Security

### Audit Status

- ✅ Code review completed
- ✅ Security testing performed
- ✅ Gas optimization verified
- ⏳ External audit pending

### Security Features

1. **Multi-Signature Validation**: Requires consensus from multiple validators
2. **Amount Limits**: Configurable min/max deposit amounts
3. **Emergency Controls**: Circuit breakers for critical situations
4. **Input Validation**: Comprehensive parameter validation
5. **Access Control**: Role-based permissions system

### Known Limitations

- Validator trust assumptions
- Bitcoin finality considerations
- Network availability dependencies

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow Clarity best practices
- Add comprehensive tests for new features
- Update documentation for API changes
- Ensure all tests pass before submitting

## 📚 API Reference

### Public Functions

| Function | Parameters | Description |
|----------|------------|-------------|
| `initialize-bridge` | None | Initialize bridge protocol |
| `pause-bridge` | None | Emergency pause bridge operations |
| `resume-bridge` | None | Resume bridge operations |
| `add-validator` | `validator: principal` | Add new validator |
| `remove-validator` | `validator: principal` | Remove validator |
| `initiate-deposit` | `tx-hash, amount, recipient, btc-sender` | Start deposit process |
| `confirm-deposit` | `tx-hash, signature` | Confirm deposit with signature |
| `withdraw` | `amount, btc-recipient` | Withdraw to Bitcoin |
| `emergency-withdraw` | `amount, recipient` | Emergency fund recovery |

### Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| 1000 | `ERR-NOT-AUTHORIZED` | Unauthorized access |
| 1001 | `ERR-INVALID-AMOUNT` | Invalid amount specified |
| 1002 | `ERR-INSUFFICIENT-BALANCE` | Insufficient balance |
| 1003 | `ERR-INVALID-BRIDGE-STATUS` | Invalid bridge state |
| 1004 | `ERR-INVALID-SIGNATURE` | Invalid signature |
| 1005 | `ERR-ALREADY-PROCESSED` | Transaction already processed |
| 1006 | `ERR-BRIDGE-PAUSED` | Bridge is paused |

## 🗺️ Roadmap

### Phase 1: Core Infrastructure ✅

- [x] Basic bridge functionality
- [x] Validator management
- [x] Deposit/withdrawal operations
- [x] Security controls

### Phase 2: Advanced Features 🚧

- [ ] Multi-chain support
- [ ] Automated rebalancing
- [ ] Fee optimization
- [ ] Advanced monitoring

### Phase 3: Ecosystem Integration 📋

- [ ] DeFi protocol integrations
- [ ] Yield farming strategies
- [ ] Governance token
- [ ] Mobile applications

## 📄 License

This project is licensed under the ISC License. See the [LICENSE](LICENSE) file for details.
