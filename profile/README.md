# 🌍 Ente Veedu

> **A Stellar-powered cross-border remittance platform enabling fast, secure, and affordable international money transfers directly to Indian bank accounts.**

---

## Overview

**Ente Veedu** is a blockchain-based cross-border remittance platform designed to simplify international money transfers for migrant workers and their families. By leveraging the **Stellar blockchain**, the platform enables near real-time settlement with lower transaction costs while integrating with India's banking infrastructure through **UPI**.

The platform combines blockchain technology with traditional financial systems using **Stellar Anchor services**, allowing users to send money internationally without requiring recipients to understand or interact with cryptocurrencies.

---

# Problem Statement

Traditional cross-border remittance systems suffer from several limitations:

- High transaction fees due to multiple financial intermediaries.
- Slow settlement times that may take hours or even days.
- Limited transparency regarding transaction status and exchange rates.
- Complex user experience for international transfers.
- Heavy dependence on centralized financial institutions.

These challenges particularly affect migrant workers who regularly send money to their families and require a faster, more affordable, and reliable solution.

---

# Solution

Ente Veedu addresses these challenges by utilizing the **Stellar blockchain** as the settlement layer for international transfers.

The platform converts fiat currency into digital assets through a **Stellar Anchor**, transfers value securely across the Stellar network, and converts the assets back into local currency before depositing the funds directly into the recipient's bank account via **UPI**.

This architecture significantly reduces settlement time, minimizes intermediary costs, and provides transparent transaction tracking while preserving a familiar banking experience for end users.

---

# Key Features

- 🌍 **Cross-Border Money Transfers**
  - Send money internationally using the Stellar blockchain.

- ⚡ **Near Real-Time Settlement**
  - Faster transaction processing compared to conventional remittance services.

- 💸 **Low Transaction Costs**
  - Reduced fees through blockchain-based settlement.

- 🏦 **UPI Bank Integration**
  - Direct payout to recipients' Indian bank accounts.

- 🔗 **Stellar Anchor Integration**
  - Seamless fiat-to-digital asset and digital asset-to-fiat conversion.

- 🔐 **Secure User Authentication**
  - Protected user accounts and secure transaction workflows.

- 📊 **Transaction Tracking**
  - Monitor transfer status throughout the remittance process.

- 📱 **Modern Web Interface**
  - Responsive application for initiating and managing transfers.

- 🧩 **Modular Microservice Architecture**
  - Independent services for wallet management, banking integration, and Anchor operations.

- 📈 **Scalable Design**
  - Architecture designed to support expansion to additional countries and payment networks.

---

# Technology Stack

| Layer          | Technologies                   |
| -------------- | ------------------------------ |
| Frontend       | Next.js, React, TypeScript     |
| Backend        | Node.js, Express               |
| Blockchain     | Stellar Network                |
| Wallet         | Stellar SDK                    |
| Database       | SQLite / PostgreSQL            |
| Authentication | JWT                            |
| Banking        | UPI (Bank Integration)         |
| APIs           | Stellar Anchor (SEP Protocols) |

---

# Architecture

```text
                 Sender
                    │
                    ▼
        Ente Veedu Web Application
                    │
                    ▼
          Stellar Anchor Service
                    │
                    ▼
             Stellar Blockchain
                    │
                    ▼
        Receiving Anchor Service
                    │
                    ▼
            UPI / Indian Bank
                    │
                    ▼
                Recipient
```

---

# Repository Structure

```text
Ente-Veedu
├── ente-veedu-wallet          # Frontend application
├── anchor-service             # Stellar Anchor implementation
├── anchor-platform            # Anchor platform services
├── bank-app                   # Banking / UPI integration
└── docs                       # Project documentation
```

---

# Vision

To make international remittances **faster, more affordable, and universally accessible** by combining the efficiency of blockchain technology with existing banking infrastructure.

---

# Contributors

Developed as part of the **Ente Veedu** project.

---

# License

This project is released under the **MIT License**.
