# 🏡 Ente Veedu 

> **Fast, secure, and affordable cross-border remittance from the Gulf to Kerala using the Stellar blockchain.**

---

# Product Description

Ente Veedu Wallet is a blockchain-powered remittance platform that enables users in Gulf countries to send money to beneficiaries in India quickly and securely. The platform leverages the Stellar network and USDC to facilitate low-cost international transfers while integrating with traditional banking infrastructure through a custom Anchor implementation.

The solution abstracts blockchain complexity from end users, providing a familiar digital payment experience while benefiting from Stellar's fast settlement and minimal transaction costs.

---

# Problem Statement

Millions of expatriates regularly send money to their families. Existing remittance systems suffer from:

- High transaction fees
- Slow settlement times
- Poor exchange transparency
- Multiple intermediaries
- Limited accessibility

Traditional international transfers can take hours or days and often involve significant service charges.

---

# Solution

Ente Veedu Wallet bridges traditional banking and blockchain.

Instead of routing money through multiple intermediaries, the platform uses Stellar as the settlement layer.

Workflow:

1. Sender initiates a remittance.
2. Funds are tokenized into USDC.
3. Transfer occurs on the Stellar blockchain.
4. The Anchor converts digital assets into local currency.
5. The recipient receives money directly into their bank account.

This architecture enables:

- Near-instant settlement
- Lower fees
- Secure blockchain transactions
- Transparent transfer tracking

---

# ✨ Product Features

## 🌍 Instant Cross-Border Remittances
Transfer money from the Gulf to India within seconds using the Stellar blockchain, providing a faster and more affordable alternative to traditional remittance services.

---

## 💸 Low Transaction Fees
Leverages Stellar's efficient blockchain infrastructure to minimize transaction costs, making international transfers economical for users.

---

## 💵 USDC-Powered Stable Transfers
Uses **USDC stablecoin** for settlement, ensuring price stability while eliminating the volatility commonly associated with cryptocurrencies.

---

## ⚡ Near Real-Time Settlement
Transfers are confirmed and settled within seconds, allowing recipients to receive funds almost instantly.

---

## 🏦 Seamless Bank Integration
Bridges blockchain and traditional banking by enabling users to deposit and withdraw funds through integrated banking services.

---

## 👥 Beneficiary Management
Users can securely add, manage, and reuse beneficiary accounts for faster repeat transactions.

---

## 📜 Transaction History & Tracking
Provides complete visibility into transfer history, including transaction status, timestamps, wallet activity, and blockchain confirmations.

---

## 🔒 Secure Wallet Infrastructure
Implements secure authentication, encrypted communication, protected wallet operations, and transaction validation to safeguard user assets.

---

## 🌐 Stellar Blockchain Integration
Built on the **Stellar Network**, enabling secure, reliable, and high-speed cross-border financial transactions.

---

## 🔄 Fiat-to-Blockchain Bridge
Converts fiat currency into USDC for international transfers and seamlessly converts it back into local currency for recipient withdrawals.

---

## 📱 Modern Responsive User Interface
Developed with **Next.js**, delivering a clean, responsive, and mobile-friendly experience across desktop and mobile devices.

---

## 🧩 Modular & Scalable Architecture
Designed with independent components—including the Wallet, Anchor Service, and Bank Service—to simplify maintenance, scalability, and future feature expansion.

---

## 🚀 Cloud Deployment
Hosted on **Vercel** with continuous deployment support, ensuring high availability, scalability, and reliable performance.

---


# System Architecture

```
                    +----------------------+
                    |   Sender (Gulf)      |
                    +----------+-----------+
                               |
                               |
                    Ente Veedu Wallet
                               |
                               |
                     Stellar Blockchain
                               |
                     Anchor Service
                               |
                     Banking Service
                               |
                    Recipient Bank Account
```

---

# Architectural Diagrams

## Overall Architecture

> TODO: Add Architecture Diagram

```
docs/architecture/system-architecture.png
```

---

## Component Diagram

> TODO: Add UML Component Diagram

```
docs/architecture/component-diagram.png
```

---

## Sequence Diagram

> TODO: Add UML Sequence Diagram

```
docs/architecture/sequence-diagram.png
```

---

## Deployment Diagram

> TODO: Add Deployment Diagram

```
docs/architecture/deployment-diagram.png
```

---

# Smart Contract Details

## Network

**Stellar Mainnet**

## Contract ID

```
TODO
```

## Explorer

```
https://stellar.expert/
```

## Screenshot

> TODO

```
docs/contracts/mainnet-contract.png
```

---

# Product Demo

## Live Application

```
https://YOUR-VERCEL-LINK.vercel.app
```

## Demo Video

```
https://youtu.be/YOUR_VIDEO
```

---

# Repository Structure

```
src/
public/
components/
lib/
hooks/
app/
styles/
docs/
```

---

# Installation

## Clone

```bash
git clone https://github.com/Ente-Veedu/Ente_Veedu_Wallet.git
```

## Install

```bash
npm install
```

## Environment

Create:

```
.env.local
```

Example

```env
NEXT_PUBLIC_STELLAR_NETWORK=testnet
NEXT_PUBLIC_HORIZON_URL=https://horizon-testnet.stellar.org

DATABASE_URL=...

SECRET_KEY=...
```

---

## Run

```bash
npm run dev
```

Visit

```
http://localhost:3000
```

---

# Product Setup Guide

## Step 1

Clone repository.

## Step 2

Install dependencies.

## Step 3

Configure environment variables.

## Step 4

Start development server.

## Step 5

Connect Anchor service.

## Step 6

Begin sending and receiving transactions.

---

# Future Vision

The long-term vision for Ente Veedu is to become a global cross-border financial infrastructure built on Stellar.

Future enhancements include:

- Production banking integrations
- UPI integration
- MoneyGram Access integration
- Multi-currency support
- Real-time exchange rates
- Mobile applications
- QR payments
- Merchant payments
- Non-custodial wallet support
- AI-powered fraud detection
- Global remittance corridors beyond India

---

# Contributors

- Robert Reji
- Team Ente Veedu

---

# License

This project is licensed under the MIT License.