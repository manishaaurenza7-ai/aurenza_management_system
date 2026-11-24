# Aurenza Academy — Vercel deployment package

This is a static-site deployment of the supplied Aurenza Academy Business & GST Invoice Portal.

## Deploy to Vercel

### Option 1 — GitHub (recommended)
1. Extract this ZIP.
2. Create a new GitHub repository and upload the contents of this folder.
3. In Vercel, select **Add New → Project** and import that repository.
4. Framework preset: **Other**.
5. Build command: leave empty.
6. Output directory: leave empty (the project root contains `index.html`).
7. Deploy.

### Option 2 — Vercel CLI
Install the Vercel CLI, sign in, open this folder in a terminal, and run:

```bash
vercel
```

For a production deployment:

```bash
vercel --prod
```

## Included
- `index.html` — the portal UI and client-side application.
- `vercel.json` — static hosting configuration and basic security headers.
- `.gitignore` — ignores local Vercel metadata.

## Important production-readiness notes

This package is deployable on Vercel as a **static application**, but the original app is not a secure multi-user ERP backend yet:

1. **Login is client-side only.** The Admin/Employee PIN values and role checks live in browser JavaScript. They are not real authentication and must not be used to protect confidential business data.
2. **Data is stored in browser localStorage.** Records are local to each browser/device. They do not automatically sync across users or devices. Export JSON backups regularly.
3. **Webhook sync is browser-side.** Do not put a private API key or privileged credential in the HTML or browser configuration. Use a server-side API route and validate requests before connecting a production database.
4. **Seed data must be reviewed.** The initial company GSTIN, PAN, CIN, contact details, address, bank details, PIN hints, and sample customer/vendor/invoice records are carried over from the supplied HTML. Verify or replace every value before using the portal for real billing.
5. **GST compliance needs review.** Validate HSN/SAC codes, place-of-supply logic, tax rates, invoice numbering, required invoice fields, and credit/debit-note handling with your accountant/CA before issuing statutory invoices.

## Recommended next step for a real business deployment

For multiple staff members and shared records, upgrade this static frontend to a full-stack app:
- Next.js (or another server-rendered framework) on Vercel
- Supabase/PostgreSQL for persistent shared records
- Supabase Auth or another server-side authentication provider
- Role-based authorization enforced on the server/database
- Server-side API routes for invoice operations and webhook integrations
- Automated database backups and audit logging

The current ZIP intentionally preserves the supplied portal's existing screens and workflows rather than silently replacing its business logic or seed data.
