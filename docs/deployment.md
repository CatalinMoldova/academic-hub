# Deployment

## Production (Vercel — recommended)

The live site at [academichub.md](https://www.academichub.md) is deployed on Vercel. Deployments are automatic on every push to `main`.

### Setup

1. Connect the `academic-hub` repository to a Vercel project.
2. Set your custom domain to `academichub.md` in the Vercel dashboard.
3. Add the environment variables from `.env.example` in **Project Settings → Environment Variables**.

No workflow file is needed — Vercel's GitHub integration handles CI/CD.

## Environment Variables

| Variable | Description |
|---|---|
| `NEXT_PUBLIC_SITE_URL` | Full public URL, e.g. `https://www.academichub.md` |
| `EMAIL_USER` | Gmail address used to send notifications |
| `EMAIL_APP_PASSWORD` | Gmail App Password (not your account password) |
| `GOOGLE_APPS_SCRIPT_URL` | Deployed web-app URL from Google Apps Script |

### Gmail App Password

1. Enable 2-Step Verification on the Gmail account.
2. Go to **Google Account → Security → App Passwords**.
3. Create a password for **Mail** and paste it into `EMAIL_APP_PASSWORD`.

## Google Sheets Integration

The enrollment and contact forms push leads to a Google Sheet via a deployed Apps Script web app.

1. Open the Google Sheet you want to use.
2. Go to **Extensions → Apps Script**.
3. Paste the contents of `integrations/google-sheets/google-apps-script.js`.
4. Click **Deploy → New deployment → Web app**.
5. Set **Execute as: Me** and **Who has access: Anyone**.
6. Copy the deployment URL and set it as `GOOGLE_APPS_SCRIPT_URL`.
7. Run the `setupSheet()` function once to create column headers.

See `integrations/google-sheets/google-apps-script.js` for the full script.

## CI

Every push and pull request runs the CI workflow in `.github/workflows/ci.yml`:

```bash
npm ci
npm run lint
npm run typecheck
npm run build
```

## Local Development

```bash
cp .env.example .env.local   # fill in your values
npm install
npm run dev                  # http://localhost:3000
```
