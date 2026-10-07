# Evidence — Provider keys re-inserted (repo BakareAhmad/DeChimexNotificationsFixed.git)

All files come from ONE clean final run: `bash e2e/provider-keys/run_final.sh keysfinal`
(fresh in-memory apps, fresh stubs, fresh evidence folder). Key values are never logged.

| Stage | Result | File |
|---|---|---|
| Full test suite | 929/929 (486 unit + 443 integration) | final-test-log.txt |
| Packaging-guard validations | 14/14 | final-packaging-guard-log.txt |
| /health (app A, REAL api.paystack.co) | Healthy — database, paystack "HTTP 200", brevo (stub) | final-health-log.txt |
| Keys + design-review journey (app A) | 36/36 | final-e2e-log.txt, shots 01–16 |
| Brevo api-key header on every outbound send | 4/4 match configured key | final-brevo-key-audit-log.txt |
| Direct-checkout / Paystack journey (app B, Paystack stub) | 60/60 | final-checkout-e2e-log.txt, shots 17–37 |
| Paystack Authorization header (initialize ×4, refund ×1) | all match configured secret | final-paystack-auth-log.txt |
| Hero regression (9 viewports + 14 responsive checkpoints, alpha/no-box, header search, PNG fallback) | 383/383 | final-hero-regression-log.txt |
| Footer placement regression | 404/404 | final-footer-e2e-log.txt |
| Notification read-state / audience + live design-review cards + error pages regression (fixes journey, app B) | 58/58 | final-fixes-e2e-log.txt |
| Secret-leak sweep over evidence/ | clean (only the PUBLIC pk_test_ key appears, shot 01) | — |

## Screenshots (01–37, ordered from the single final run)
- `01-config-endpoint-paystack-public-key.png` — `/api/v1/config` serves the Paystack PUBLIC key, no secrets
- `02-owner-logged-in.png` — owner signed in
- `03-customer-verified-signed-in.png` — customer registered → Brevo OTP → verified → signed in
- `04-customer-workspace-empty-design-reviews.png`, `05-staff-workspace-open.png` — empty customer/staff workspaces
- `06-customer-uploaded-v1.png`, `07-staff-sees-v1-live.png` — v1 upload, staff sees it live
- `08-staff-approved-v1.png`, `09-customer-sees-approval-live.png` — approve → customer sees approval live
- `10-staff-sees-v2-live-independent-history.png` — v2 live (independent history)
- `11-reject-requires-reason-validation.png` — VALIDATION: reject requires a reason
- `12-staff-rejected-v2-with-reason.png`, `13-customer-sees-rejection-reason-live.png` — rejected with reason, customer sees it live
- `14-invalid-file-type-refused.png` — VALIDATION: `.exe` refused (400 "File type '.exe' is not allowed")
- `15-customer-workspace-final-persisted.png`, `16-staff-workspace-final-persisted.png` — history persists after reload (customer + staff)
- `17-checkout-catalog-filter.png` .. `21-checkout-checkout-amounts.png` — catalog filter, direct vs custom buy actions, cart guard rejects custom product, checkout amounts
- `22-checkout-direct-order-placed.png`, `23-checkout-direct-paid.png` — order placed → Paystack → paid
- `24-checkout-direct-workspace-no-design-steps.png` .. `27-checkout-direct-lifetime-spending.png` — workspace, admin badge, activity log, lifetime spend
- `28-checkout-review-unlocked-after-purchase.png`, `29-checkout-review-locked-unpurchased.png` — review unlocked after purchase / locked when unpurchased
- `30-checkout-direct-payment-failed.png` — VALIDATION: payment failed state
- `31-checkout-direct-retry-paid.png`, `32-checkout-direct-cancelled.png`, `33-checkout-direct-refunded.png` — retry paid, cancelled, refunded
- `34-checkout-custom-workspace-assigned.png` .. `36-checkout-custom-paid.png` — custom order: assigned workspace, admin badge, paid
- `37-checkout-my-orders-coherent.png` — My orders coherent

The previous root evidence set (2026-10-06 notification read-state run, 13 shots + log + README) was preserved at `e2e/fixes/evidence-final-run/` before this run. Earlier email-design evidence remains at `e2e/email-ux/evidence-final-run/` and implementation-fixes evidence at `e2e/impl-fixes/evidence-final-run/`.
