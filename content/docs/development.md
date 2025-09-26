+++
title = 'Development'
date = '2025-09-26T21:03:00+10:00'
draft = false
+++

## Tooling

- **Package manager:** Bun (preferred) or PNPM
- **Formatting & linting:** [Biome](https://biomejs.dev/) (`bunx biome format --write .`, `bun run lint`)
- **Type checking:** `bun run typecheck`
- **Testing:** `bun run test`

## Recommended workflow

1. Start services if needed:

   ```bash
   docker-compose up -d
   bun run db:migrate
   bun run dev
   ```

2. Work inside feature branches (`git checkout -b feature/your-feature`).
3. Keep pull requests focused and reference GitHub issues when possible.
4. Run linting/formatting before opening a PR.

## Preview refactor status

The preview panel currently renders DOM elements for real-time feedback. A binary renderer is in development to align preview and export output. Avoid heavy work on:

- Preview rendering and effects
- Export pipeline internals

Good contribution areas include timeline UX, project management, performance improvements, accessibility, and documentation.

## Architecture highlights

- **Editor state:** [Zustand](https://github.com/pmndrs/zustand) stores in `apps/web/src/stores/*`.
- **Media pipeline:** FFmpeg.js for in-browser processing, background removal via Python (`apps/bg-remover`), transcription via Modal (`apps/transcription`).
- **Storage:** IndexedDB + Origin Private File System for local media, with optional Cloudflare R2 integration.
- **Desktop:** Tauri wrapper shares React components from `apps/web`.

### State management stores

- `editor-store.ts` — canvas presets, guides, bootstrap routines.
- `timeline-store.ts` — tracks, timeline elements, playback state.
- `media-store.ts` — imported media catalogue and metadata.
- `playback-store.ts` — transport controls and timing.
- `project-store.ts` — project persistence, autosave.
- `panel-store.ts` — UI layout and panel visibility.
- `keybindings-store.ts` — keyboard shortcut registry.
- `sounds-store.ts` / `stickers-store.ts` — audio cues and overlay assets.

## Support packages

- `packages/ui` — headless UI primitives used across apps.
- `packages/config` — shared ESLint, TypeScript, and Next.js configuration.
- `packages/types` — TypeScript definitions shared across services.

## Media tooling

- **FFmpeg** — client-side processing via `@ffmpeg/ffmpeg`.
- **Background removal** — Python services (U2Net, SAM, Gemini) in `apps/bg-remover`.
- **Transcription** — Modal-based Whisper pipeline documented in [Transcription service](/docs/transcription).

## Release cadence

- Changes merge to `main` behind feature flags where necessary.
- Desktop builds are produced manually while the Tauri pipeline is under construction.
- Public web deploys use Vercel previews before promotion.

Don’t hesitate to open a draft pull request early — reviewers can help with architecture decisions and API design.
