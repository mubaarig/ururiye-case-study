# ururiye-case-study
Case study for a Somali-first POS and business management app built with React Native, Expo, Firebase, offline queues, staff roles, inventory, debts, expenses, and reports.


# Ururiye — Somali-first Business Management App

Ururiye is a Somali-first business management and POS app designed for small shops, pharmacies, markets, restaurants, and local businesses in Somaliland.

The app helps business owners move away from notebooks, memory, and scattered WhatsApp messages by managing daily business operations from one mobile app.

> The production source code is private because Ururiye is an active commercial product.  
> This repository is a public case study showing the product, architecture, technical decisions, and engineering work.

---

## Product Overview

Ururiye helps small business owners manage:

- Sales
- Products and stock
- Customer debts
- Supplier debts
- Expenses
- Profit tracking
- Staff roles
- Reports
- Receipts
- Offline business activity

The goal is simple: give Somali-speaking shop owners a reliable business system that works on their phone, in their language, and in real daily conditions.

---

## Tech Stack

- React Native
- Expo
- TypeScript
- Firebase Authentication
- Firestore
- Firebase Security Rules
- Firebase Cloud Functions
- Offline queued writes
- Role-based access control
- Jest / React Native Testing Library
- Firebase emulator tests

---

## Core Features

### Sales

Owners and staff can record daily sales, including:

- Cash sales
- Mobile money sales
- Credit sales
- Product-based sales
- Receipt generation
- Cost of goods sold tracking
- Estimated profit calculation

Sales are designed with idempotent writes to reduce duplicate transaction risk when the app is offline or the network is unstable.

---

### Inventory Management

Ururiye includes product and stock management for small businesses.

Features include:

- Add and edit products
- Track stock quantity
- Low-stock alerts
- Buying price and selling price
- Stock history
- Stock adjustment requests
- Approval workflow for sensitive stock changes

This helps owners understand what is available, what is running low, and where stock changes came from.

---

### Debt Tracking

The app separates two important debt types:

- **Customer debt** — money customers owe the business
- **Supplier debt** — money the business owes suppliers

This distinction is important for local business owners because many shops sell on credit and also buy stock from suppliers on delayed payment terms.

---

### Expenses

Owners can record daily business expenses such as:

- Rent
- Transport
- Staff costs
- Utilities
- Supplies
- Other operating costs

Expenses are included in dashboard and reporting calculations.

---

### Staff Roles and Permissions

Ururiye supports multiple user roles:

- Owner
- Manager
- Worker

Permissions are enforced both in the UI and Firestore security rules.

Example restrictions:

- Workers can record sales and operational activity
- Managers can access reports and supplier-related workflows
- Owners control staff access and business settings

---

### Reports

Ururiye provides business insights such as:

- Daily sales
- Monthly sales
- Expenses
- Profit estimate
- Outstanding debts
- Low-stock products
- Staff activity
- Stock changes

The reports are designed to help non-technical business owners understand their business quickly.

---

## Offline-first Design

Many target users may experience unstable mobile networks. Ururiye is designed with offline-tolerant workflows.

The app uses queued writes for important business actions. When the device reconnects, pending writes are flushed safely.

Key offline considerations:

- Queue writes locally
- Attach client write IDs
- Prevent duplicate sales
- Retry failed writes
- Drop repeatedly failed writes after a safe limit
- Flush only writes belonging to the current authenticated user

---

## Architecture

```mermaid
flowchart TD
    A[React Native Mobile App] --> B[Auth Layer]
    A --> C[Offline Queue]
    C --> D[Firestore Writes]
    A --> E[Business Logic Layer]
    E --> F[Sales]
    E --> G[Inventory]
    E --> H[Debts]
    E --> I[Expenses]
    E --> J[Reports]
    D --> K[Firestore Database]
    K --> L[Security Rules]
    K --> M[Cloud Functions]
    M --> N[Audit Logs]

This README documents the engineering behind a private production application. It intentionally omits source code, Firebase configuration, credentials, customer data, and internal business logic.
