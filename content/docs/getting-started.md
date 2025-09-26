+++
title = 'Getting Started'
date = '2025-09-26T21:03:00+10:00'
draft = false
+++

## Prerequisites

- [Node.js](https://nodejs.org/en/) 18+
- [Bun](https://bun.sh/docs/installation) (preferred package manager)
- [Docker](https://docs.docker.com/get-docker/) + [Docker Compose](https://docs.docker.com/compose/install/) for optional services

> **Tip:** Bun handles the workspace dependencies used by OpenCut. If you run into `workspace:*` errors with npm, upgrade to npm 9+ or switch to Bun/PNPM.

## Clone and bootstrap

```bash
git clone https://github.com/OpenCut-app/OpenCut.git
cd OpenCut

# App web frontend
cd apps/web
cp .env.example .env.local
bun install
bun run dev
```

The development server runs at <http://localhost:3000>.

## Environment variables

```bash
# Database (matches docker-compose.yaml)
DATABASE_URL="postgresql://opencut:opencutthegoat@localhost:5432/opencut"

# Better Auth
BETTER_AUTH_SECRET="your-generated-secret-here"
NEXT_PUBLIC_BETTER_AUTH_URL="http://localhost:3000"

# Redis
UPSTASH_REDIS_REST_URL="http://localhost:8079"
UPSTASH_REDIS_REST_TOKEN="example_token"

# Optional blogging integration
MARBLE_WORKSPACE_KEY=cm6ytuq9x0000i803v0isidst
NEXT_PUBLIC_MARBLE_API_URL=https://api.marblecms.com

NODE_ENV="development"
```

Generate the secret with one of these commands:

```bash
openssl rand -base64 32               # Unix/macOS
node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"  # cross-platform
```

## Optional: database + Redis

```bash
# From the repo root
docker-compose up -d

# Apply migrations from apps/web
bun run db:migrate
```

## Project layout

```
apps/
├── web/               # Next.js application
├── desktop/           # Tauri desktop client
├── bg-remover/        # Python background removal pipeline
└── transcription/     # Audio transcription service

packages/
├── config/            # Shared configuration (eslint, tsconfig, etc.)
├── ui/                # Reusable UI components
└── ...
```

## Next steps

- Configure optional [transcription](/docs/transcription) support.
- Read the [development guide](/docs/development) for contribution workflows.
- Explore the roadmap and issues on [GitHub](https://github.com/OpenCut-app/OpenCut/issues).
