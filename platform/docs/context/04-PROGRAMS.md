# REVA — Pluggable Programs

## Program Registry

| Program | Code | Status | Public URL |
|---------|------|--------|------------|
| Bữa Cơm Nhà | FRESH_ORDER | Active | event.reva.com/bua-com-nha/ |
| Flash Sale | FLASH_SALE | Future | — |
| Pre-Order | PRE_ORDER | Future | — |
| Subscription | SUBSCRIPTION | Future | — |

## Lifecycle

1. Admin registers program in Program Registry (slug, rules, date range)
2. `reva-order` loads program config for order engine
3. Next.js renders `/[slug]/` from CMS/API — **platform core unchanged**
4. End of season: deactivate program; historical orders retained

## Seasonal swap

Swap = toggle program + deploy static pages. Core services (membership, inventory, rule) stay running.
