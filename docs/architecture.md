# Architecture

## Overview

AcademicHub is a Next.js 15 App Router application. All routing is file-based under `src/app/`. Server-side logic lives exclusively in API route handlers; the rest of the app is client-rendered React.

## Request Flow

```
Browser
  │
  ├── Page request  → Next.js App Router → src/app/**/page.tsx
  │                                         └── src/components/  (shared UI)
  │
  └── Form submit   → fetch()  → src/app/api/**/route.ts
                                    ├── Validate input
                                    ├── Send email via Nodemailer  (src/lib/email.ts)
                                    └── POST to Google Apps Script → Google Sheets
```

## Pages

| Route | File | Purpose |
|---|---|---|
| `/` | `src/app/page.tsx` | Homepage — hero, benefits, testimonials, FAQ |
| `/cursuri` | `src/app/cursuri/page.tsx` | Six courses for grades 9 and 12 |
| `/profesori` | `src/app/profesori/page.tsx` | Teacher profiles |
| `/simulare` | `src/app/simulare/page.tsx` | Exam simulation registration |
| `/despre` | `src/app/despre/page.tsx` | About, mission, methodology |
| `/contact` | `src/app/contact/page.tsx` | Contact form |
| `/rezolvari` | `src/app/rezolvari/page.tsx` | Worked solutions |
| `/termeni` | `src/app/termeni/page.tsx` | Terms and conditions |

## API Routes

| Endpoint | Handler | Action |
|---|---|---|
| `POST /api/enroll` | `src/app/api/enroll/route.ts` | Course enrollment |
| `POST /api/simulare` | `src/app/api/simulare/route.ts` | Exam simulation signup |
| `POST /api/contact` | `src/app/api/contact/route.ts` | Contact form submission |

All three routes validate the request body server-side, send an email notification, and forward the payload to Google Sheets via the Apps Script web-app URL in `GOOGLE_APPS_SCRIPT_URL`.

## Components

| Component | Purpose |
|---|---|
| `Header` | Site-wide navigation with mobile hamburger menu |
| `Footer` | Links, company info, social contacts |
| `Button` | Reusable CTA button with variant support |
| `CourseCard` | Displays course name, grade, price, and CTA |
| `EnrollmentModal` | Overlay form — course selection + contact fields |

## Lead Management

Submissions from all three API routes are mirrored into Google Sheets using the Apps Script integration in `integrations/google-sheets/`. See `docs/deployment.md` for setup.
