# REVA — Security & Rate Limit

## 3-layer security

| Layer | Location | Controls |
|-------|----------|----------|
| Gateway | reva-gateway | JWT validate, CORS, rate limit, WAF-ready |
| Service | Each API | Authorization policies, input validation |
| Data | Per DB | Tenant scope, PII encryption at rest |

## Rate limits (gateway)

| Client | Limit | Window |
|--------|-------|--------|
| Public event API | 60 req | /min / IP |
| Authenticated staff | 300 req | /min / user |
| POS webhook | 120 req | /min / store key |

## Token types

| Token | Issuer | Use |
|-------|--------|-----|
| User JWT | reva-auth | reva.com MFE |
| Service token | reva-auth | service-to-service |
| Partner embed | reva-auth | dashboard iframe |
| ERP JWT | Linm auth | `company_id` on vouchers |

## Audit & PII

- Append-only audit log for wallet / order mutations
- Mask phone/email on list APIs; full on detail + permission
- GDPR-style export/deletion hooks on reva-membership (Phase 2+)
