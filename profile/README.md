<div align="center">

# 🏡 Ente Veedu

### Fast, secure, and affordable cross-border remittance from the Gulf to Kerala — built on Stellar

[![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat&logo=next.js&logoColor=white)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Stellar](https://img.shields.io/badge/Stellar-7D00FF?style=flat&logo=stellar&logoColor=white)](https://stellar.org/)
[![USDC](https://img.shields.io/badge/USDC-2775CA?style=flat&logo=circle&logoColor=white)](https://www.circle.com/usdc)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](#license)

[Live Demo](#-product-demo) · [Features](#-key-features) · [Architecture](#-system-architecture) · [Getting Started](#-getting-started) · [Roadmap](#-roadmap)

</div>

---

## 📖 Overview

**Ente Veedu** ("Ente Veedu" — Malayalam for _"my home"_) is a blockchain-powered remittance platform that lets Gulf-based expatriates send money home to Kerala in seconds, not days. It uses the **Stellar network** and **USDC** as a settlement layer, paired with a custom Anchor implementation that bridges digital assets to real bank accounts — so users get the speed and cost benefits of blockchain rails without ever needing to understand blockchain.

## 🎯 The Problem

Millions of expatriates send money home every month. Today, that process is:

| Pain Point                 | Impact                                              |
| -------------------------- | --------------------------------------------------- |
| High transaction fees      | Traditional corridors charge 3–7% per transfer      |
| Slow settlement            | Transfers can take hours to multiple business days  |
| Poor exchange transparency | Hidden FX margins on top of stated fees             |
| Multiple intermediaries    | Correspondent banks add cost and delay at every hop |
| Limited accessibility      | Cash pickup and banking-hour dependencies           |

## 💡 The Solution

Ente Veedu replaces the intermediary chain with a single settlement layer: Stellar.

```mermaid
flowchart LR
    A["📱 Sender"] --> B["🏡 Ente Veedu Wallet"]
    B --> C["⭐ Stellar Network"]
    C --> D["🏦 Anchor"]
    D --> E["👨 Recipient"]

    style C fill:#7D00FF,color:#fff
```

This gives senders **near-instant settlement**, **lower fees**, and **full transfer transparency**, while recipients still get money the way they always have — straight into their bank account.

---

## ✨ Key Features

| Feature                                | Description                                                                  |
| -------------------------------------- | ---------------------------------------------------------------------------- |
| 🌍 **Instant Cross-Border Remittance** | Transfers settle on Stellar in seconds instead of days                       |
| 💸 **Low Transaction Fees**            | Stellar's minimal network fees replace multi-hop correspondent banking costs |
| 💵 **USDC-Powered Stability**          | Settlement in USDC avoids crypto volatility during transfer                  |
| 🏦 **Seamless Bank Integration**       | Deposit and withdraw through a connected Anchor/banking service              |
| 👥 **Beneficiary Management**          | Save and reuse recipient details for faster repeat transfers                 |
| 📜 **Transaction History & Tracking**  | Full visibility into status, timestamps, and blockchain confirmations        |
| 🔒 **Secure Wallet Infrastructure**    | Authenticated sessions, encrypted communication, validated transactions      |
| 🧩 **Modular Architecture**            | Independent Wallet, Anchor, and Bank services for easier scaling             |
| 📱 **Responsive UI**                   | Built with Next.js + Tailwind for a clean cross-device experience            |
| 🚀 **Cloud-Native Deployment**         | Seamless scaling across Vercel and standalone services                       |

---

## 🛠 Tech Stack

| Layer          | Technology                                         |
| -------------- | -------------------------------------------------- |
| **Frontend**   | Next.js, React, TypeScript, Tailwind CSS           |
| **Backend**    | Next.js API Routes, Node.js                        |
| **Blockchain** | Stellar Network, Stellar SDK, Horizon API, Soroban |
| **Database**   | Supabase / PostgreSQL (production)                 |
| **Deployment** | Vercel / Railway                                   |

---

## 🏗 System Architecture

> [!TIP]
> Follow the numbered steps (**1** through **6**) to trace the lifecycle of a remittance transfer. Card colors represent the client app (green), Next.js BFF (blue), database (orange), Stellar blockchain (purple), and the anchor / banking adapters (red & light blue).

```mermaid
flowchart TD
    %% Nodes and Styles
    classDef client fill:#dcfce7,stroke:#166534,stroke-width:1.5px,color:#14532d;
    classDef api fill:#dbeafe,stroke:#1e40af,stroke-width:1.5px,color:#1e3a8a;
    classDef db fill:#fef3c7,stroke:#92400e,stroke-width:1.5px,color:#78350f;
    classDef chain fill:#f3e8ff,stroke:#6b21a8,stroke-width:1.5px,color:#581c87;
    classDef anchor fill:#fee2e2,stroke:#991b1b,stroke-width:1.5px,color:#7f1d1d;
    classDef bank fill:#e0f2fe,stroke:#075985,stroke-width:1.5px,color:#0c4a6e;

    Client["📱 Ente Veedu (Client App)<br/>(Local Wallet, Web Crypto & Local Signing)"]:::client
    BFF["⚙️ Ente Veedu (Next.js BFF)<br/>(Remittance logic, username cache, cron indexers)"]:::api
    DB[("🗄️ Supabase DB (PostgreSQL)<br/>(Transaction logs, contacts & encrypted keys)")]:::db
    Stellar["⭐ Stellar Network (Testnet)<br/>(Horizon API, USDC asset & Soroban username registry)"]:::chain
    Anchor["🏦 anchor-service (SEP Adapter)<br/>(Stellar Anchor Platform + Observer & Watcher daemons)"]:::anchor
    BankSim["🏛️ enteVeedu-Bank (Bank Simulator)<br/>(Instant UPI ID verification & bank payouts)"]:::bank

    %% Client Flows
    Client -->|"1. Setup, Register & Resolve User"| BFF
    Client -->|"3. Submit USDC Payment with reference_id"| Stellar
    Client -->|"4. Confirm Tx Hash / Trigger Payout"| BFF

    %% BFF Backend Flows
    BFF -->|"2. Validate Recipient / 5. Initiate Payout"| BankSim
    BFF -->|"Read/Write Records & Cache"| DB
    BFF -->|"Verify Payment & Query Registry"| Stellar

    %% Anchor & Fallback Observer Flows
    Anchor -->|"Poll incoming USDC deposits/withdrawals"| Stellar
    Anchor -->|"6. Payout (Fallback Daemon)"| BankSim
    Anchor -->|"Update Remittance Status"| DB

    %% Final Settlement
    BankSim --> Recipient(["👨 Recipient Bank Account (INR)"]):::bank
```

### Production Deployment Architecture

```mermaid
flowchart TD
    %% Nodes and Styles
    classDef browser fill:#dcfce7,stroke:#166534,stroke-width:1.5px,color:#14532d;
    classDef vercel fill:#f3f4f6,stroke:#1f2937,stroke-width:1.5px,color:#111827;
    classDef railway fill:#fae8ff,stroke:#86198f,stroke-width:1.5px,color:#701a75;
    classDef supabase fill:#ecfdf5,stroke:#047857,stroke-width:1.5px,color:#064e3b;
    classDef network fill:#f3e8ff,stroke:#6b21a8,stroke-width:1.5px,color:#581c87;

    subgraph UserSpace ["🌐 Client Browser / Device"]
        Browser["Ente Veedu Web UI<br/>(Client-side AES-GCM Encryption & Local SDK Signing)"]:::browser
    end

    subgraph VercelHost ["▲ Vercel Cloud (Ente Veedu App)"]
        BFF["Ente Veedu Backend (BFF)<br/>(Next.js API Serverless Routes)"]:::vercel
    end

    subgraph VercelHostBank ["▲ Vercel Cloud (enteVeedu-Bank Sim)"]
        BankSim["enteVeedu-Bank API<br/>(Bank Simulator Next.js App)"]:::vercel
    end

    subgraph RailwayHost ["🚂 Railway App Platform (Docker Containers)"]
        AnchorSvc["anchor-service (SEP Adapter)<br/>(Node.js Daemon Service)"]:::railway
        AnchorPlatform["Stellar Anchor Platform (AP)<br/>(Java/Kotlin SEP-24 Engine)"]:::railway
    end

    subgraph SupabaseHost ["⚡ Supabase Platform (Cloud DB)"]
        Postgres[("PostgreSQL Database<br/>(Tables, Username Caches & Logs)")]:::supabase
    end

    subgraph StellarHost ["⭐ Stellar Network (Decentralized Ledger)"]
        Nodes["Stellar Horizon Nodes & Soroban RPC"]:::network
        Contract["Soroban Username Registry Contract"]:::network
    end

    %% Network / Protocol Lines
    Browser -->|HTTPS / Next.js Actions| BFF
    Browser -->|JSON-RPC / Web Crypto| Nodes
    
    BFF -->|Postgres Protocol| Postgres
    BFF -->|JSON-RPC / HTTPS| Nodes
    BFF -->|HTTPS / REST| BankSim
    
    AnchorPlatform -->|JSON-RPC / Horizon API| Nodes
    AnchorSvc -->|Platform RPC / Webhooks| AnchorPlatform
    AnchorSvc -->|HTTP REST API| BankSim
    AnchorSvc -->|Horizon Event Stream| Nodes
    AnchorSvc -->|Postgres Connection| Postgres
    
    BankSim -->|Instant UPI Payouts| Recipient(["👨 Recipient VPA / Bank Account"])
```

### Remitanance Transfer Sequence

```mermaid
sequenceDiagram
    participant S as  Sender
    participant W as Ente Veedu Wallet
    participant BFF as Backend (BFF)
    participant DB as Supabase DB
    participant St as Stellar Network
    participant An as anchor-service
    participant B as enteVeedu-Bank (UPI)

    S->>W: 1. Input Recipient UPI & Amount
    W->>BFF: 2. Initiate Remittance (/api/remittance/initiate)
    BFF->>B: Validate Recipient UPI
    B-->>BFF: Validated (Recipient Name)
    BFF->>DB: Insert transaction record (status: pending)
    BFF-->>W: Return remittance details & reference_id
    W->>W: 3. Build & Cryptographically Sign Tx Locally
    W->>St: 4. Submit USDC payment to Anchor Address with memo reference_id
    St-->>W: Tx confirmed on-chain

    alt Happy Path (Client-Driven Confirmation)
        W->>BFF: 5. Confirm Tx Hash (/api/remittance/confirm)
        BFF->>St: Verify transaction memo, amount & status
        BFF->>DB: Update status: pending -> processing
        BFF->>B: 6. Trigger Instant Payout (transfer ID & reference_id)
        B-->>BFF: Payout Completed
        BFF->>DB: Update status: processing -> completed
        BFF-->>W: Payout complete notification
        W-->>S: Transfer complete!
    else Fallback Path (Daemon Payment Watcher)
        Note over An: Runs in background every 5 seconds
        An->>St: Poll incoming payments to Anchor Address
        St-->>An: Detect incoming payment with memo reference_id
        An->>DB: Lookup pending remittance matching reference_id
        An->>DB: Update status: pending -> payment_detected -> processing
        An->>B: 6. Trigger Fallback Payout (transfer ID & reference_id)
        B-->>An: Payout Completed
        An->>DB: Update status: processing -> completed
    end
```

---

## ⛓️ Blockchain Integration Details

| Item               | Value                                                                               |
| ------------------ | ----------------------------------------------------------------------------------- |
| Network            | Stellar (Testnet for development, Mainnet for production)                           |
| Settlement Asset   | USDC                                                                                |
| Anchor Standards   | SEP-10 (Web Auth), SEP-24 (Interactive Deposit & Withdrawal)                        |
| Explorer Link      | [Stellar Expert Explorer](https://stellar.expert/explorer/testnet)                  |
| Soroban Usage      | On-Chain Username Registry (stores unique @usernames linked to Stellar Public Keys) |
| Cron Sync Interval | Indexes registration events from Soroban RPC sequence and caches to Supabase        |

---

## 🔐 Security & Compliance

### Client-Side Cryptographic Custody

- Private keys and seeds are generated client-side inside the user's browser.
- Encrypted using **AES-GCM (256-bit)** with **PBKDF2 key derivation (100,000 iterations)**.
- Encrypted payload (salt, IV, ciphertext) is stored in the database for cross-device access.
- **The server never sees or stores plaintext private keys or user passwords**. All transaction signing happens client-side.

### Compliance & Verification Roadmap

- **Jurisdictional Gates:** Allow/Block lists restricting outbound corridors (UAE/GCC) to inbound corridors (Kerala/India).
- **KYC Integration (SEP-12 / Third-Party):** Integration points for customer onboarding, identity document processing, and validation.
- **Sanctions Screening:** Daily screening of senders and recipients against OFAC/UN sanctions lists.
- **MSB Licensing:** Architected to integrate with fully-regulated local financial anchors and U.S./UAE remittance partners.

---

## 🚀 Getting Started

Ente Veedu relies on a multi-service structure to orchestrate client wallets, anchor platforms, and local banking simulations.

### Prerequisites

- Node.js 18+ & npm
- A supabase database with the remittance schemas applied

### 1. Database Setup

Create tables in your database using the migration files:

```bash
# Apply migrations to your Supabase PostgreSQL instance
# supabase-migration-remittance.sql
# supabase-migration-update.sql
```

### 2. Multi-Service Configuration

This repository requires three components running in parallel for full testing:

1. **`stellar-pay` (Ente Veedu)** (Next.js client + BFF)
2. **`anchor-service`** (Anchor observation engine & SEP webhooks)
3. **`bank-sim` (enteVeedu-Bank)** (Simulated bank accounts, balances, and UPI payouts)

#### Run `bank-sim` (enteVeedu-Bank Simulator API)

```bash
cd bank-sim
npm install
npm run dev
# Running on http://localhost:3001
```

#### Run `anchor-service` (Stellar platform daemon)

```bash
cd anchor-service
npm install
npm run dev
# Running on http://localhost:3003
```

#### Run `stellar-pay` (Ente Veedu Main application)

```bash
cd stellar-pay
npm install
cp .env.example .env.local
# Fill in required variables in .env.local
npm run dev
# Running on http://localhost:3000
```

### Environment Variables Template

Create a `.env.local` inside the `stellar-pay` (Ente Veedu) directory:

```env
# Stellar network config
NEXT_PUBLIC_STELLAR_NETWORK=testnet
NEXT_PUBLIC_HORIZON_URL=https://horizon-testnet.stellar.org
NEXT_PUBLIC_RPC_URL=https://soroban-testnet.stellar.org
NEXT_PUBLIC_FRIENDBOT_URL=https://friendbot.stellar.org

# USDC Asset Configuration
NEXT_PUBLIC_USDC_ISSUER=GAJ553PWUPQDOJBP33JKEHXJXCGT5QTU7U245Y243MMQUA4QBQIJ55ND

# Sponsor / Registry Contract ID
NEXT_PUBLIC_REGISTRY_CONTRACT_ID=CDY...
SPONSOR_SECRET_KEY=S...

# Database Configuration (Supabase)
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJ...
SUPABASE_SERVICE_ROLE_KEY=ey...

# Bank Simulator Connection
BANK_URL=http://localhost:3001
BANK_API_KEY=your-bank-api-key

# Cron Secret for Indexer Authorization
CRON_SECRET=your-cron-secret
```

---

## 📁 Project Structure

```
stellar-pay (Ente Veedu)/
├── src/
│   ├── app/                # Pages & BFF API Routes
│   │   ├── api/            # API Endpoints (faucet, register, remittance, resolve)
│   │   └── layout.tsx
│   ├── components/         # SendMoneyModal, Onboarding, BalanceCard, etc.
│   ├── context/            # WalletContext.tsx (Web Crypto & SDK core state)
│   ├── hooks/              # custom React hooks (useFreighter.ts)
│   └── lib/                # Adapters & Services
│       ├── services/       # bankService, exchangeRateService, remittanceService
│       ├── crypto.ts       # Browser PBKDF2/AES-GCM encryption
│       ├── stellar.ts      # Horizon client instances & balance query logic
│       └── wallet.ts       # Local storage wallet helpers
```

---

## 🎬 Product Demo

|                      |                                           |
| -------------------- | ----------------------------------------- |
| **Live Application** | `https://ente-veedu.vercel.app`           |
| **Demo Video**       | `https://youtu.be/ente-veedu-walkthrough` |

---

## 🗺 Roadmap

### Completed Features

- [x] Client-side encrypted non-custodial wallet generation (AES-GCM / PBKDF2).
- [x] Live exchange rates with automatic 30s locked quote refreshes.
- [x] Integrated real-time UPI ID validation against the bank simulator.
- [x] On-chain registry indexing daemon to query custom @usernames on Soroban.
- [x] Automatic payment-watcher daemon for out-of-sync / offline transactions.

### Future Work

- [ ] Direct MoneyGram Access endpoints for local cash pick-up.
- [ ] Multi-currency support (AED, SAR, QAR to INR).
- [ ] Non-custodial freighter wallet hardware link.
- [ ] Advanced AI-powered transaction risk scoring.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome. Feel free to open an issue or submit a pull request.

## 👥 Contributors

- **Robert Reji**
- Team Ente Veedu

## 📄 License

This project is licensed under the [MIT License](LICENSE).
