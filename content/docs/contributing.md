+++
title = 'Contributing'
date = '2025-09-26T21:03:00+10:00'
draft = false
+++

# Contributing to OpenCut

Thank you for your interest in contributing to OpenCut! This document provides guidelines and instructions for contributing.

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/en/) (v18 or later)
- [Bun](https://bun.sh/docs/installation) (preferred package manager)
- [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/) for optional services

> **Note:** Docker is optional but required for running the local database and Redis services. If you are only working on the frontend you can skip Docker.

### Setup

1. Fork the repository
2. Clone your fork locally
3. Navigate to the web app directory: `cd apps/web`
4. Copy `.env.example` to `.env.local`
5. Install dependencies: `bun install`
6. Start the development server: `bun run dev`

If you see an error like `Unsupported URL Type "workspace:*"` when running `npm install`, upgrade npm to v9+ or use Bun/PNPM.

## Where to Focus

**Great areas:** timeline and project management improvements, performance tuning, bug fixes, accessibility, documentation, and tests.

**Avoid for now:** preview rendering, export pipeline internals, and major preview UI overhauls (a binary renderer is being developed).

Unsure? Ask in [Discord](https://discord.gg/zmR9N35cjK) or open an issue.

## Local development

```bash
# Start database + Redis services
docker-compose up -d

# Apply migrations from apps/web
bun run db:migrate

# Run the app
bun run dev
```

Populate `.env.local` with the values documented in the [getting started guide](/docs/getting-started).

## Quality checks

```bash
bun run lint
bun run typecheck
bunx biome format --write .
bun run test
```

## Submitting changes

1. Create a topic branch: `git checkout -b feature/your-feature`
2. Make changes and add tests where relevant
3. Run linting/formatting checks
4. Commit with a descriptive message and open a pull request

Please follow the [Code of Conduct](/docs/code-of-conduct) and keep discussions respectful.
