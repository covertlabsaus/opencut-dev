+++
title = "Point OpenCut to a Remote Postgres"
description = "Configure OpenCut to use a managed Postgres database with SSL and pooled connections."
draft = false
+++

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "@id": "https://opencut.dev/faq/opencut-remote-postgres",
    "name": "How do I point OpenCut to a remote Postgres database?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Set DATABASE_URL in apps/web/.env.local to the remote URI with sslmode=require, restart bun dev, and run bun run db:migrate so Drizzle deploys the schema remotely."
    }
  }]
}
</script>

Managed Postgres services (Supabase, Railway, Neon, RDS) work once the connection string is updated.

## Example configuration

```env
DATABASE_URL="postgresql://user:password@db.example.com:5432/opencut?sslmode=require"
POOL_MIN=1
POOL_MAX=10
```

Reload the Next.js server so the new variables apply.

## Apply migrations

```bash
cd apps/web
bun run db:migrate
```

Drizzle will create tables remotely. Verify with `psql`:

```bash
psql "$DATABASE_URL" -c '\dt'
```

## Recommended flags
- Add `statement_timeout=60000` if exports run long.
- Use connection pooling (pgBouncer) to stay within limits.
- Store credentials in your platform secret manager instead of `.env.local` when deploying.

## Diagram

```mermaid
flowchart LR
    A[OpenCut Next.js] -->|Prisma client| B[pgBouncer]
    B --> C[Managed Postgres]
```

Monitor connection counts in your provider dashboard to ensure the editor does not exhaust limits.
