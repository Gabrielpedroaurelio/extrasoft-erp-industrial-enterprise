# AgroMetal ERP

> Enterprise Resource Planning system built for a mid-sized Angolan metalworking manufacturer — managing Stock, HR, Finance, and Sales in a single integrated platform.

---

## Overview

AgroMetal ERP is a full-stack ERP system developed from scratch for **AgroMetal Lda.**, a metalworking company based in Luanda, Angola, with ~140 employees operating across 3 production lines.

The company previously managed all operations through Excel spreadsheets, WhatsApp, and paper — resulting in production stoppages from undetected stock shortages, payroll errors affecting 5–8% of employees monthly, and zero real-time financial visibility.

This system replaces those manual processes with an integrated platform covering the four core business areas.

---

## Modules

| Module | Description | Status |
|--------|-------------|--------|
| **Stock** | Product catalog, stock movements, low-stock alerts, inventory reports | 🔵 In development |
| **HR** | Employee records, attendance tracking, monthly payroll processing | ⏳ Planned |
| **Finance** | Accounts payable/receivable, cash flow, monthly reports | ⏳ Planned |
| **Sales** | Customer management, quotations, invoicing with PDF export | ⏳ Planned |

---

## Tech Stack

### Backend
![Node.js](https://img.shields.io/badge/Node.js-20-339933?style=flat&logo=nodedotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=flat&logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?style=flat&logo=postgresql&logoColor=white)
![Express](https://img.shields.io/badge/Express-4-000000?style=flat&logo=express&logoColor=white)

- **Runtime**: Node.js 20 + TypeScript (strict mode)
- **Framework**: Express.js
- **Database**: PostgreSQL 16 — raw SQL with `node-postgres (pg)`, no ORM
- **Auth**: JWT (access token 15min + refresh token 7 days) + RBAC
- **Validation**: Zod
- **Architecture**: Clean Architecture (Domain → Application → Infrastructure → Interfaces)

### Frontend
![React](https://img.shields.io/badge/React-18-61DAFB?style=flat&logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=flat&logo=typescript&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-3-06B6D4?style=flat&logo=tailwindcss&logoColor=white)

- **Framework**: React 18 + TypeScript
- **Styling**: Tailwind CSS
- **Data fetching**: React Query (TanStack Query)
- **HTTP client**: Axios with request/response interceptors
- **Routing**: React Router v6 with protected routes

### Infrastructure
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat&logo=docker&logoColor=white)

- **Local dev**: Docker Compose (PostgreSQL + API)
- **Logging**: Winston (structured JSON logs)
- **Deploy**: Railway (staging), self-hosted LAN server (production)

---

## Architecture

This project follows **Clean Architecture** principles — business logic is completely decoupled from frameworks, databases, and HTTP.

```
src/
├── domain/                  # Business entities and rules — no external dependencies
│   ├── entities/            # Product, Employee, Transaction, Order...
│   ├── repositories/        # Repository interfaces (contracts)
│   └── value-objects/       # Money, SKU, Email...
│
├── application/             # Use cases — orchestrate domain + repositories
│   ├── use-cases/
│   │   ├── stock/           # CreateProduct, UpdateStock, GetLowStock...
│   │   ├── hr/              # CreateEmployee, ProcessPayroll...
│   │   ├── financial/       # CreateTransaction, GetCashFlow...
│   │   └── sales/           # CreateSale, GenerateInvoice...
│   └── dtos/
│
├── infrastructure/          # Concrete implementations
│   ├── database/
│   │   ├── migrations/      # Raw SQL migration files
│   │   └── repositories/    # PostgreSQL implementations using pg
│   └── services/            # Email, storage, PDF generation
│
├── interfaces/              # HTTP layer — the only layer that knows Express
│   └── http/
│       ├── controllers/
│       ├── routes/
│       ├── middlewares/      # auth, rbac, error handler
│       └── validators/       # Zod schemas
│
└── shared/                  # Errors, utils, types
```

---

## Access Control (RBAC)

| Role | Stock | HR | Finance | Sales |
|------|-------|----|---------|-------|
| `admin` | Full | Full | Full | Full |
| `manager` | Full | Full | Read | Full |
| `warehouse` | Full | — | — | Read |
| `hr` | Read | Full | Read | — |
| `accountant` | Read | Payroll | Full | Read |
| `sales` | Read | — | — | Full |

---

## Project Status

```
Phase 0 — Discovery & Requirements     ████████░░  80%  ← User Stories in progress
Phase 1 — System Design & Architecture ░░░░░░░░░░   0%  ← Next
Phase 2 — Project Setup                ░░░░░░░░░░   0%
Phase 3 — Backend Development          ░░░░░░░░░░   0%
Phase 4 — Frontend Development         ░░░░░░░░░░   0%
Phase 5 — Testing & QA                 ░░░░░░░░░░   0%
Phase 6 — Deploy & Observability       ░░░░░░░░░░   0%
```

**Timeline**: 24 weeks · 8h/week · Solo developer  
**Minimum viable portfolio milestone**: Week 7 (Stock module complete)

---

## Documentation

All project documentation lives in the [`/docs`](./docs) folder:

| Document | Description |
|----------|-------------|
| [`BRD_AgroMetal_ERP.pdf`](./docs/BRD_AgroMetal_ERP.pdf) | Business Requirements Document — problem statement, stakeholders, success criteria |
| [`roadmap.html`](./docs/roadmap.html) | Full engineering roadmap — phases, Gantt chart, calendar, MoSCoW, user stories, ERD preview, ADRs |
| [`ADR-001`](./docs/adr/ADR-001-raw-sql.md) | Why raw SQL with pg instead of Prisma |
| [`ADR-002`](./docs/adr/ADR-002-clean-architecture.md) | Why Clean Architecture instead of simple MVC |
| [`ADR-003`](./docs/adr/ADR-003-jwt.md) | Why stateless JWT instead of Redis sessions |
| [`ADR-004`](./docs/adr/ADR-004-uuid.md) | Why UUID instead of sequential IDs |

---

## Getting Started

> ⚠️ The project is currently in the planning phase. Setup instructions will be added when Phase 2 begins.

### Prerequisites

- Node.js 20+
- Docker + Docker Compose
- PostgreSQL 16 (via Docker)

### Local Development

```bash
# Clone the repository
git clone https://github.com/your-username/erp-agrometalurgica.git
cd erp-agrometalurgica

# Start the database
docker-compose up -d db

# Install dependencies
npm install

# Run migrations
npm run migrate

# Start the development server
npm run dev
```

---

## Business Context

**Client**: AgroMetal Lda. *(fictional company — created for study and portfolio purposes)*  
**Sector**: Metalworking / Industrial manufacturing  
**Location**: Luanda, Angola  
**Size**: ~140 employees, 3 production lines, double shift (6am–10pm)  
**Core problems solved**:
- Production stoppages from undetected stock shortages (2–3/month)
- Manual payroll processing taking 3–4 days with ~5–8% error rate
- Zero real-time financial visibility — decisions made without knowing current cash flow
- Sales pipeline and invoicing with no traceability

---

## Author

Built by a self-taught developer based in Luanda, Angola — learning enterprise software engineering by building real systems.

Currently studying: TypeScript · Node.js · PostgreSQL · Clean Architecture · System Design

---

*This project is being built as a portfolio piece and learning exercise following professional software engineering practices — from requirements discovery through deploy.*