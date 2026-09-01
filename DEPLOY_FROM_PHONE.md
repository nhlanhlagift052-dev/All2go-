# All2Go Sandbox deployment

1. Create a PRIVATE GitHub repository named `all2go`.
2. Upload the files in this folder to the repository.
3. Create/sign in to Render and choose New -> Web Service.
4. Connect GitHub and select the `all2go` repository.
5. Build command: `npm install`
6. Start command: `npm start`
7. Add environment variables:
   PAYFAST_SANDBOX=true
   PAYFAST_MERCHANT_ID=<your Sandbox Merchant ID>
   PAYFAST_MERCHANT_KEY=<your Sandbox Merchant Key>
   PAYFAST_PASSPHRASE=<your private Sandbox passphrase>
   APP_BASE_URL=<your Render HTTPS URL>
   JWT_SECRET=<a long random secret>
8. Deploy.
9. Open `<your Render URL>/api/health`. It should show `payment_mode: "sandbox"`.

The ITN endpoint will be:
`<your Render HTTPS URL>/api/payfast/itn`

Never put Payfast credentials in source code or GitHub. Never share your Payfast password, OTP, PIN, or banking details.

This is a Sandbox/test deployment. SQLite is suitable only for this MVP test; Render's default filesystem is ephemeral, so a real launch should use persistent production storage.
