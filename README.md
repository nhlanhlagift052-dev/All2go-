# All2Go v7 — Payfast Sandbox Payment Integration

This version replaces the fake "demo payment" with a Payfast-hosted checkout integration.

Payfast's official developer docs describe a custom checkout that posts to the Payfast hosted payment page, uses a security signature, and confirms payment through an ITN. The sandbox is intended for testing without real money. The integration here follows that model.

## Environment variables

Required for sandbox:
```bash
PAYFAST_MERCHANT_ID=your_sandbox_merchant_id
PAYFAST_MERCHANT_KEY=your_sandbox_merchant_key
PAYFAST_PASSPHRASE=your_sandbox_passphrase
PAYFAST_SANDBOX=true
APP_BASE_URL=https://YOUR_PUBLIC_HTTPS_DOMAIN
JWT_SECRET=use-a-long-random-secret
```

The Payfast credentials belong in environment variables, NOT in the source code.

## Run

```bash
npm install
npm start
```

For local browser testing:
`http://localhost:3000`

For ITN testing, the server must be publicly reachable. Payfast notes that local servers cannot receive ITNs because the notification must reach the server from Payfast.

## Payment flow

1. Customer creates an All2Go order.
2. All2Go calculates the amount from its database.
3. All2Go creates a signed Payfast checkout form.
4. Customer is redirected to Payfast.
5. Payfast sends an ITN to `/api/payfast/itn`.
6. All2Go verifies signature, merchant ID and amount, then asks Payfast's validation endpoint to confirm the transaction.
7. Only after validation does All2Go mark the order `paid`.

## Important
The Payfast Sandbox does not move real money. Do not put live credentials into testing.

Before live launch:
- HTTPS
- Live Payfast merchant verification
- Live credentials in a secret manager
- Production hosting
- Monitoring and backups
- Strong admin security/MFA
- POPIA/privacy/terms/refund policies
- Payment reconciliation
- Merchant payout/commission accounting
- Delivery integration
- Business verification and appropriate platform agreements


## Before deploying
- Change/remove the demo admin credentials in `server.js` before any public launch.
- Keep all Payfast credentials and `JWT_SECRET` only in Render environment variables.
- This package is for sandbox testing; SQLite on ephemeral hosting is not suitable for production data.
