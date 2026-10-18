# 3Quarters PDF Converter

Customers add pictures, pay 75¢ each through Stripe Checkout, and get them back as PDF, JPG, PNG or WEBP.
Conversion only runs on the server after Stripe confirms payment, and only up to the number of pictures paid for.

## Run it locally
1. Install Node 18 or newer.
2. `npm install`
3. Copy `.env.example` to `.env` and paste in your Stripe **test** secret key.
4. `npm start`, then open http://localhost:3000
5. Pay with test card 4242 4242 4242 4242 (any future date, any CVC).

## Put it online
Host it on any Node host (Render, Railway, Fly.io, a VPS).
- Build command: `npm install`  Start command: `npm start`
- Set the environment variables from `.env.example`. `BASE_URL` must be your public https address.
- Switch to your live Stripe key (`sk_live_...`) when you're ready to take real money.

## Things to know
- At 75¢ a picture, a single-picture order clears Stripe's $0.50 minimum.
- Stripe's fee is about 2.9% + 30¢ per payment, so a 1-picture order nets roughly 43¢. Raise `MIN_PICTURES` (e.g. 2 for $1.50) for a better margin per payment.
- PDFs are one picture per page-sized file, scaled to fit an A4 page length.
- Order credits are tracked in Stripe session metadata, so no database is needed.
- Add a privacy policy and terms before launch. Pictures are processed in memory and never saved.
