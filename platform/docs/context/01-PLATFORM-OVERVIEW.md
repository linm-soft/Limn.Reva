# REVA Platform — Overview

## 1. What is REVA?

REVA is a retail platform for Foodmart / REVA Mart supermarket chains. It connects POS, membership, orders, inventory, and Linm ERP without replacing existing systems on day one.

> REVA = Retail Core (membership · order · inventory · rules) + Event-Job Bus + Pluggable seasonal programs + Linm ERP

**Audience:** Operations, marketing, investors (pitch via `platform/index.html`).

## 2. Core Principles

| # | Principle | Technical meaning |
|---|-----------|-------------------|
| 1 | Enter once | Domain data owned by one service; no duplicate master |
| 2 | Event-driven sync | Cross-service via event-job (PostgreSQL), not chatty sync |
| 3 | Program plug-in | Seasonal campaigns (Bữa Cơm Nhà) without core rewrite |
| 4 | Two surfaces | `reva.com` (staff/partner) + `event.reva.com` (public SEO) |
| 5 | API gateway | Single entry `api.reva.com` — JWT, rate limit, YARP |
| 6 | DB per service | No cross-DB joins; IDs + HTTP or denormalized reads |
| 7 | ERP boundary | Linm ERP = accounting, statutory reports, store tenants |
| 8 | Bilingual UX | VI default; EN for investor / partner docs |

## 3. Domain Map

| Domain | App | Type | Access |
|--------|-----|------|--------|
| reva.com | single-spa shell + 5 MFEs | Staff / partner | JWT login |
| event.reva.com | Next.js SSG/ISR/CSR | Public campaigns | No login |
| api.reva.com | reva-gateway (YARP) | API | Bearer JWT |
| ERP | Linm ERP MFE | Finance / ops | company_id tenant |
