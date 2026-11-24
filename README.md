<div align="center">

<img src="https://raw.githubusercontent.com/Studio1HQ/Studio1HQ/main/assets/banners/Antigravity-experiment.webp" alt="Antigravity E-Commerce Experiment: A full-stack store with guest checkout and abandoned cart emails" width="100%" />

<br />
<br />

# Antigravity E-Commerce Experiment

### A full-stack store with guest checkout and abandoned cart emails

An e-commerce experiment named Antigravity: a React storefront, an Express and Prisma backend, guest checkout and cron-driven abandoned cart emails sent with Resend.

<br />

[![Built by Studio1](https://img.shields.io/badge/Built_by_Studio1-f97316?style=for-the-badge&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxNjAgMTYwIiBmaWxsPSJub25lIj48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTAgMzVDMCAxNi42ODA3IDE0LjA3NDQgMS42NDg0NCAzMiAwLjEyNjk1M1YxNDFINTEuMDUyM0M1Mi40MzA4IDEzNy4zNDQgNTQuNzQ0NiAxMzMuNjg5IDU3Ljk5MzggMTMwLjAzM0M2MS4xNDQ2IDEyNi41MDggNjQuNjg5MiAxMjMuNDQgNjguNjI3NyAxMjAuODI5QzcyLjU2NjIgMTE4LjM0OSA3Ni4zNTY5IDExNi43ODIgODAgMTE2LjEyOVY4Ni43NTQ0Qzc1LjQ3MDggODcuOTI5MiA3MS4zODQ2IDg5LjY5MTkgNjcuNzQxNSA5Mi4wNDE1QzY0IDk0LjUyMjUgNjAuNzUwOCA5Ny40NiA1Ny45OTM4IDEwMC44NTRDNTYuNTM0NSAxMDIuNzIgNTUuMjU0NSAxMDQuNjU5IDU0LjE1MzkgMTA2LjY3MVYwSDEyNUMxNDQuMzMgMCAxNjAgMTUuNjY5OSAxNjAgMzVWMTI1QzE2MCAxNDQuMzMgMTQ0LjMzIDE2MCAxMjUgMTYwSDEyNFYxOEgxMDQuOTQ4QzEwMy41NjkgMjEuNjgxNiAxMDEuMjU1IDI1LjM2MjggOTguMDA2MiAyOS4wNDQ0Qzk0Ljg1NTQgMzIuNTk0MiA5MS4zMTA4IDM1LjY4NDEgODcuMzcyMyAzOC4zMTRDODMuNDMzOCA0MC44MTIgNzkuNjQzMSA0Mi4zODk2IDc2IDQzLjA0NzRWNzIuNjMwNEM4MC41MjkyIDcxLjQ0NzMgODQuNjE1NCA2OS42NzI0IDg4LjI1ODUgNjcuMzA1N0M5MiA2NC44MDc2IDk1LjI0OTIgNjEuODQ5MSA5OC4wMDYyIDU4LjQzMDdDOTkuNDY1NSA1Ni41NTEzIDEwMC43NDUgNTQuNTk4NiAxMDEuODQ2IDUyLjU3MjNWMTYwSDM1QzE1LjY3IDE2MCAwIDE0NC4zMyAwIDEyNVYzNVoiIGZpbGw9IiNmZmZmZmYiLz48L3N2Zz4K)](https://studio1hq.com)

[More examples](https://github.com/Studio1HQ) &nbsp;·&nbsp; [studio1hq.com](https://studio1hq.com)

</div>

<br />

## Overview

A full-stack e-commerce experiment built under the name Antigravity. It has a React storefront with guest checkout and an Express backend that emails shoppers who leave items in their cart. A cron job finds abandoned carts and sends an HTML reminder through [Resend](https://resend.com).

It is useful as a worked example of the abandoned-cart flow, from cart API to scheduled email.

## Features

- **Guest checkout**: no account is needed to buy.
- **Abandoned cart recovery**: a cron job runs every 15 minutes and emails shoppers with product images, quantities, prices, the cart total and a link back to checkout.
- **Cart API**: create or get a cart, add items, set the cart email and check out.
- **Connection resilience**: retry with exponential backoff (3 attempts), 10-second request timeouts and a connection status banner in the UI.
- **Logging and health checks**: request logging, cart and email operation logs, and `GET /health` with database status.
- **Email fallback**: falls back to Ethereal for emails when Resend is not configured.
- **Tests**: a test script for email sending and curl examples for the cart API.

## Tech stack

| Layer | Tool |
| --- | --- |
| Frontend | [React](https://react.dev), TypeScript, [Vite](https://vite.dev), [Tailwind CSS](https://tailwindcss.com) |
| UI | [shadcn/ui](https://ui.shadcn.com), React Router, Sonner |
| Backend | [Node.js](https://nodejs.org) with [Express](https://expressjs.com) |
| Database | [Prisma](https://www.prisma.io) with SQLite |
| Email | [Resend](https://resend.com) |
| Scheduling | node-cron |

## Getting started

### Prerequisites

- Node.js 18 or later and npm
- A [Resend](https://resend.com) API key

### Installation

```bash
git clone https://github.com/Studio1HQ/Antigravity-experiment.git
cd Antigravity-experiment
npm install
cd backend && npm install
cd ../frontend && npm install
cd ../backend
cp .env.example .env
npx prisma generate
npx prisma db push
```

### Environment variables

Edit `backend/.env`.

| Variable | Description |
| --- | --- |
| `DATABASE_URL` | Prisma database URL. Use `file:./dev.db` for SQLite in development. |
| `RESEND_API_KEY` | Resend API key from [resend.com/api-keys](https://resend.com/api-keys). Verify your domain in Resend for production. |
| `PORT` | Optional backend port, 4000 by default. |

### Run

Start both servers from the project root with the root script:

```bash
npm run dev
```

Or run them separately:

```bash
cd backend && npm run dev
cd frontend && npm run dev
```

- Frontend: [http://localhost:5173](http://localhost:5173)
- Backend: [http://localhost:4000](http://localhost:4000)
- Health check: [http://localhost:4000/health](http://localhost:4000/health)

Test email sending and the cart API:

```bash
cd backend
node src/test-email.js your-email@example.com

curl -X POST http://localhost:4000/api/cart -H "Content-Type: application/json" -d '{}'
curl -X POST http://localhost:4000/api/cart/items -H "Content-Type: application/json" \
  -d '{"cartId":"YOUR_CART_ID","productId":"1","quantity":1,"price":299.99}'
```

## How it works

1. The user browses products and adds to the cart (`POST /api/cart/items`).
2. The user enters an email (`POST /api/cart/email`).
3. If they leave, the cart stays active.
4. The cron job in `backend/src/services/cronService.js` runs every 15 minutes (`*/15 * * * *`), finds abandoned carts and sends the email.
5. The email links back to checkout, and the purchase completes with `POST /api/cart/checkout`.

| Endpoint | Purpose |
| --- | --- |
| `POST /api/cart` | Create or get a cart |
| `POST /api/cart/items` | Add an item |
| `POST /api/cart/email` | Update the cart email |
| `POST /api/cart/checkout` | Complete checkout |
| `GET /` | API status |
| `GET /health` | Health check with database status |

To change the schedule, edit `cronService.js`. To change the email template or colors, edit `sendAbandonedCartEmail` in `backend/src/services/resendService.js`. To add products, edit `frontend/src/data/products.ts` and `backend/src/data/products.js`.

```text
frontend/   React storefront (components, CartContext, pages, config.ts)
backend/    Express API (controllers, routes, services, Prisma schema)
```

The backend also includes `services/tensorlake.js` and a receipt controller. Both are mock stubs that log events and return sample items. They do not call a live API.

For production, use PostgreSQL or MySQL, set `DATABASE_URL`, run `npx prisma migrate deploy`, deploy the backend to a Node host, build the frontend with `npm run build` for static hosting and set `API_BASE_URL` in `frontend/src/config.ts`.

## Resources

- [Resend](https://resend.com): email API used for reminders.
- [Prisma](https://www.prisma.io): ORM for the cart data.
- [shadcn/ui](https://ui.shadcn.com): UI components.
- [Pixabay](https://pixabay.com): source of the product images.

<br />

---

<div align="center">

<a href="https://studio1hq.com">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Studio1HQ/website/main/brand/studio1-logo-on-dark.svg" />
    <img src="https://raw.githubusercontent.com/Studio1HQ/website/main/brand/studio1-logo-on-light.svg" alt="Studio1" width="160" />
  </picture>
</a>

Built by **[Studio1](https://studio1hq.com)**, the technical content and DevRel partner for devtool teams.<br />
Browse more open-source examples at [github.com/Studio1HQ](https://github.com/Studio1HQ).

[![Website](https://img.shields.io/badge/studio1hq.com-0b0807?style=for-the-badge&logo=googlechrome&logoColor=white)](https://studio1hq.com)
[![Book a call](https://img.shields.io/badge/Book_a_strategy_call-f97316?style=for-the-badge&logo=googlecalendar&logoColor=white)](https://cal.com/studio1/collab)
[![X](https://img.shields.io/badge/%40Studio1HQ-141414?style=for-the-badge&logo=x&logoColor=white)](https://x.com/Studio1HQ)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0a66c2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/company/studio1hq/)

<sub><a href="https://studio1hq.com">studio1hq.com</a> · Technical content, docs, video and DevRel for devtools</sub>

</div>
