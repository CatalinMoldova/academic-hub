# AcademicHub.md — Production Website for a Moldovan Math School

Production full-stack EdTech website for [AcademicHub.md](https://www.academichub.md), a mathematics preparation school in Chișinău, Moldova, serving 100+ active students preparing for national exams.

![Next.js](https://img.shields.io/badge/Next.js-15.4.6-black?logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?logo=typescript)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4-38bdf8?logo=tailwindcss)
![Vercel](https://img.shields.io/badge/Deployed-Vercel-black?logo=vercel)

## Live Website

[academichub.md](https://www.academichub.md)

## Business Context

AcademicHub.md prepares students in small groups for Moldovan national mathematics exams (grades 9 and 12). The platform supports course discovery, exam-simulation enrollment, student acquisition, and operational lead management. The school has helped 2,700+ students and reports a 90%+ exam success rate.

## Screenshots

> See `assets/screenshots/` for UI previews.

## Features

- **Course pages** — six math courses for grades 9 and 12, each with pricing and details
- **Teacher profiles** — bios and credentials for each instructor
- **Enrollment modal** — in-page enrollment form with client- and server-side validation
- **Exam simulation registration** — dedicated signup flow for mock exam sessions
- **Contact form** — direct messaging with email notification via Nodemailer
- **Lead management** — submissions stored via Google Sheets (Apps Script) integration
- **SEO** — per-page metadata, Open Graph tags, `sitemap.xml`, `robots.txt`
- **Responsive design** — mobile-first layout with hamburger navigation

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 15.4.6 (App Router) |
| Language | TypeScript 5 |
| Styling | Tailwind CSS 4 |
| Icons | Lucide React |
| Email | Nodemailer (Gmail App Password) |
| Lead storage | Google Sheets via Apps Script |
| Deployment | Vercel |

## Architecture

```
Browser → Next.js App Router
            ├── Page components  (src/app/**/page.tsx)
            ├── Shared components (src/components/)
            └── API routes       (src/app/api/**/route.ts)
                    ├── /api/enroll    → email notification + Google Sheets
                    ├── /api/simulare  → email notification + Google Sheets
                    └── /api/contact   → email notification
```

See [`docs/architecture.md`](docs/architecture.md) for more detail.

## Getting Started

```bash
npm install
cp .env.example .env.local   # fill in your values
npm run dev                  # http://localhost:3000
```

### Available Scripts

```bash
npm run dev        # development server with Turbopack
npm run build      # production build
npm start          # production server
npm run lint       # ESLint
npm run typecheck  # TypeScript type-check (no emit)
```

## Environment Variables

Copy `.env.example` to `.env.local` and fill in your values:

```env
NEXT_PUBLIC_SITE_URL=https://www.academichub.md
EMAIL_USER=
EMAIL_APP_PASSWORD=
GOOGLE_APPS_SCRIPT_URL=
```

See [Gmail App Passwords](https://support.google.com/accounts/answer/185833) and [`docs/deployment.md`](docs/deployment.md) for setup details.

## Repository Structure

```
academic-hub/
├── src/
│   ├── app/
│   │   ├── api/
│   │   │   ├── contact/route.ts
│   │   │   ├── enroll/route.ts
│   │   │   └── simulare/route.ts
│   │   ├── contact/page.tsx
│   │   ├── cursuri/page.tsx
│   │   ├── despre/page.tsx
│   │   ├── profesori/page.tsx
│   │   ├── rezolvari/page.tsx
│   │   ├── simulare/page.tsx
│   │   ├── termeni/page.tsx
│   │   ├── globals.css
│   │   ├── layout.tsx
│   │   └── page.tsx
│   ├── components/
│   │   ├── Button.tsx
│   │   ├── CourseCard.tsx
│   │   ├── EnrollmentModal.tsx
│   │   ├── Footer.tsx
│   │   └── Header.tsx
│   └── lib/
│       └── email.ts
├── public/
│   ├── favicon.ico
│   ├── robots.txt
│   └── sitemap.xml
├── docs/
│   ├── architecture.md
│   └── deployment.md
├── integrations/
│   └── google-sheets/
│       └── google-apps-script.js
├── assets/
│   └── screenshots/
└── .github/
    └── workflows/
        └── ci.yml
```

## Engineering Practices

- Strict TypeScript (`strict: true`)
- ESLint via `eslint-config-next`
- Reusable component library under `src/components/`
- Server-side validation on all API routes
- Environment variables for all secrets — no hardcoded credentials
- CI pipeline: lint → typecheck → build on every push and PR

## Future Improvements

- Unit tests for components (Jest + React Testing Library)
- End-to-end tests (Playwright) for enrollment and contact flows
- Google Analytics integration
- Admin dashboard for lead review
- Bilingual support (Romanian / Russian)
- CMS for course content management

## License

Proprietary — AcademicHub.md. All rights reserved.
