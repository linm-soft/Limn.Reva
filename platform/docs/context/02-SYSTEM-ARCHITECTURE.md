# REVA — System Architecture

## ASCII diagram

```
╔══════════════════════════════════════════╗
║             CLIENT LAYER                 ║
╠══════════════════╦═══════════════════════╣
║  reva.com        ║  event.reva.com       ║
║  single-spa shell║  Next.js SSG/SSR      ║
╚══════════════════╩═══════════════════════╝
          │                  │
          ▼                  ▼
╔══════════════════════════════════════════╗
║    api.reva.com — reva-gateway (YARP)    ║
╚══════════════════════════════════════════╝
    │    │    │    │    │    │    │
    ▼    ▼    ▼    ▼    ▼    ▼    ▼
 auth member order inv  rule anal notif
    │    │    │    │    │    │    │
  [db] [db] [db] [db] [db] [db] [db]

        Linm ERP (external) ← POS webhook / sync
```

## Backend services

| Service | Port | DB | Responsibility |
|---------|------|-----|----------------|
| reva-gateway | api.reva.com | — | JWT, rate limit, route |
| reva-auth | 5001 | reva_auth_db | Users, roles, tokens |
| reva-membership | 5002 | reva_member_db | Customer, wallet 3 ngăn |
| reva-order | 5003 | reva_order_db | Orders, programs, POS webhook |
| reva-inventory | 5004 | reva_inv_db | SKU, stock, reservations |
| reva-rule | 5005 | reva_rule_db | Margin, budget, approval |
| reva-analytics | 5006 | reva_analytics_db | Dashboard, reports |
| reva-notification | 5007 | reva_notif_db | Zalo, SMS, push |

## Frontend surfaces

| Route | Micro-app | Notes |
|-------|-----------|-------|
| /membership/* | reva-membership-app | 3001 |
| /orders/* | reva-order-app | 3002 |
| /inventory/* | reva-inventory-app | 3003 |
| /dashboard/* | reva-dashboard-app | 3004 |
| /admin/* | reva-admin-app | 3005 |

Public: `event.reva.com/bua-com-nha/` — SSG landing, ISR catalog, CSR order (no auth).
