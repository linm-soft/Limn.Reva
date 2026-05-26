# REVA — Dashboard

## Micro-app routes

| Route | Users | Reports |
|-------|-------|---------|
| /dashboard/executive | CEO, GĐ | Revenue, GM%, store matrix |
| /dashboard/store | Store manager | Shift sales, stock alerts |
| /dashboard/partner | Co-shop / investor | Embed token, scoped P&L |

## Report types

- Operational: orders, AOV, traffic (reva-analytics, event-sourced)
- Membership: wallet balance, top-up, redemption
- ERP (Linm): B01, store P&L per `companyId` — see `pages/phase2.html`

## Partner access

- Role `dashboard:partner`
- Embed token with expiry + store scope
- No raw PII export without audit log
