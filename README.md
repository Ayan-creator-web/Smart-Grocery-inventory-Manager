# 🛒 GrocerIQ — Smart Grocery List & Inventory Manager

A full-stack-ready web application for managing household grocery inventory with smart restocking suggestions, expiry tracking, recipe-based list generation, and price trend monitoring.

---

## 🚀 Features

| Feature | Description |
|---|---|
| **Dashboard** | KPI cards (items, low-stock, expiring, list count), stock-by-category bar chart, recent alerts, smart suggestions banner |
| **Grocery List** | Aisle-grouped checklist, add/remove items, source tagging (manual / recipe / low-stock / suggestion), search & filter |
| **Pantry** | Inventory lot cards with expiry heat badges (🟢 ok / 🟡 soon / 🔴 expired), stock progress bars, "Use" action |
| **Recipes** | Recipe cards with ingredient chips; one-click "Add to Grocery List" from recipe |
| **Price Tracker** | Per-item price history bar charts, store comparison, trend arrow (↑/↓) |
| **Alerts** | Prioritised expiry alerts, low-stock notices, weekly digest entries |
| **Household** | Multi-member management with roles (OWNER / MEMBER), invite flow |
| **Receipt OCR** | Simulated receipt parser that imports items to pantry |

---

## 🛠️ Tech Stack (Full-Stack Architecture)

```
Frontend  → HTML5 + Vanilla JS (or swap to Next.js + React)
Styling   → Custom CSS with DM Serif Display + DM Sans fonts
Backend   → Node.js / NestJS + Prisma + PostgreSQL  (as per spec)
Jobs      → BullMQ + Redis for daily expiry/restock digests
OCR       → FastAPI microservice (receipt parsing + barcode lookup)
PWA       → manifest.webmanifest + service worker (offline cache)
Auth      → JWT (bcrypt passwords, per-household row checks)
Infra     → Docker Compose (Postgres, Redis, API, Ingest, Web)
```

---

## 📂 Project Structure

```
groceriq/
├── index.html              ← This file (complete frontend demo)
│
├── apps/
│   ├── web/                ← Next.js + Tailwind PWA
│   │   └── app/
│   │       ├── dashboard/page.tsx
│   │       ├── list/page.tsx
│   │       ├── pantry/page.tsx
│   │       └── recipes/page.tsx
│   │
│   ├── api/                ← NestJS + Prisma
│   │   ├── prisma/schema.prisma
│   │   └── src/
│   │       ├── auth/
│   │       ├── households/
│   │       ├── inventory/
│   │       ├── list/
│   │       ├── recipes/
│   │       ├── prices/
│   │       ├── suggest.service.ts
│   │       └── jobs/worker.ts
│   │
│   └── ingest/             ← FastAPI OCR + Barcode
│       └── app.py
│
└── infra/
    └── docker-compose.yml
```

---

## 🏃 Running Locally

```bash
# Clone
git clone https://github.com/yourusername/groceriq.git
cd groceriq

# Open the frontend demo (no build needed)
open index.html

# Full stack (requires Docker)
docker-compose up --build
```

---

## 📊 Data Model (Prisma)

- **User** — auth, profile
- **Household** — multi-member shared space
- **HouseholdMember** — OWNER / MEMBER role
- **Item** — catalog (barcode, category, preferred aisle)
- **InventoryLot** — per-lot qty, expiry, consumed tracking
- **GroceryList / GroceryEntry** — checkable list with source tagging
- **Recipe / RecipeIngredient** — recipe-to-list automation
- **PriceHistory** — per-store price log with trends

---

## ✨ Smart Features

- **Auto-Restock Suggestions** — when `sum(qty - consumedQty) < threshold`
- **Expiry Heat Badges** — 🔴 expired / 🟠 ≤3 days / 🟢 safe
- **Recipe → List** — push all recipe ingredients to grocery list
- **Receipt OCR** — FastAPI parses items, qty, price → auto-creates lots
- **Barcode Lookup** — EAN/UPC → item name + category
- **Daily Digest Job** — BullMQ cron at 07:00 for expiry + low-stock alerts
- **Price Trend Arrows** — ↑ (more expensive) / ↓ (cheaper) vs last entry

---

## 🎯 Relevance to Industry Roles

| Role | How This Project Applies |
|---|---|
| **Data Engineer** | Prisma schema design, price history pipelines, BullMQ job orchestration |
| **Full-Stack Dev** | NestJS REST API, Next.js PWA, Prisma ORM, Redis queues |
| **ML/AI Engineer** | OCR/NER pipeline (FastAPI), usage pattern inference, restock prediction |

---

## 👤 Author

**Ayan Mukherjee** | IT Student, NSEC Kolkata (2027)  
Data Engineering Track | [LinkedIn](#) | [GitHub](#)

---


