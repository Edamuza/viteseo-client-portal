# Vite SEO Client Quotation Portal

A private Next.js app for sharing quotations with clients. Clients sign in with a one-time passcode (OTP) to view their quotes and download them as PDFs. There are no client passwords: admins generate the access codes.

## How it works

1. An admin signs in (Clerk) and manages clients and their quotations.
2. The admin generates an access code for a client.
3. The client enters the OTP, sees their quotations and downloads the PDF.

## Tech stack

- Next.js and TypeScript
- Prisma with PostgreSQL (Supabase or Neon)
- Upstash Redis
- Clerk for admin authentication
- Radix UI components
- Sentry for error monitoring
- Vitest and Playwright for tests
- Vercel for deployment

## Getting started

You need Node.js, a PostgreSQL database, an Upstash Redis instance and a Clerk application.

```bash
npm install              # also runs prisma generate
cp .env.example .env     # then fill in the values
npm run db:push          # create the tables
npm run db:seed          # optional seed data
npm run dev              # start the dev server
```

The variables in `.env.example` are grouped as database, Redis, Clerk, application URLs and security secrets (session, encryption and CSRF). Generate each secret with `openssl rand -hex 32`.

## Scripts

| Command | What it does |
| --- | --- |
| `npm run dev` | Start the development server |
| `npm run build` / `npm run start` | Build and run for production |
| `npm run lint` / `npm run lint:fix` | Run ESLint, with or without fixes |
| `npm run typecheck` | TypeScript type check |
| `npm run db:generate` | Generate the Prisma client |
| `npm run db:push` | Push the schema to the database |
| `npm run db:migrate` | Run migrations in development |
| `npm run db:migrate:deploy` | Run migrations in production |
| `npm run db:studio` | Open Prisma Studio |
| `npm run db:seed` | Seed the database |
| `npm run sync:quotes` | Run the quote sync script in `scripts/` |
| `npm test` / `npm run test:coverage` | Unit tests with Vitest |
| `npm run test:e2e` | End-to-end tests with Playwright |

## Project structure

```
app/          Next.js routes and pages
components/   UI components
lib/          Shared helpers
prisma/       Database schema and seed script
scripts/      One-off scripts (for example sync-quotes)
tests/        Unit and end-to-end tests
types/        Shared TypeScript types
docs/         Project documentation
middleware.ts Request middleware
```

## Documentation

- `docs/` holds the project documentation.
- `er_diagram.png` shows the database relationships.
- `vite-seo-complete-documentation-v2.pdf` is the full written documentation.

## Deployment

The app is configured for Vercel (see `vercel.json`). Set the same environment variables in the Vercel project and run `npm run db:migrate:deploy` against the production database.
