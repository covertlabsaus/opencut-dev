+++
date = '2025-09-26T20:58:21+10:00'
draft = false
title = 'OpenCut - Free Open Source Video Editor'
+++

<div align="center">
  <img src="/logo.png" alt="OpenCut Logo" width="100" />
  <h1>OpenCut</h1>
  <h3>A free, open-source video editor for web, desktop, and mobile.</h3>
</div>

## Why OpenCut? 🎯

- **Privacy First** 🔒 - Your videos stay on your device
- **Completely Free** 💰 - Every basic feature of CapCut is paywalled now
- **User-Friendly** ✨ - People want editors that are easy to use - CapCut proved that
- **No Watermarks** 🚫 - Professional results without branding

## ✨ Features

- **Timeline-based editing** - Professional multi-track timeline
- **Multi-track support** - Audio, video, and overlay tracks
- **Real-time preview** - See changes instantly
- **No subscriptions** - One-time setup, lifetime use
- **Cross-platform** - Web, desktop, and mobile support

## 🏗️ Architecture

```mermaid
graph TD
    A[OpenCut Editor] --> B[Web App]
    A --> C[Desktop App]
    A --> D[Mobile App]

    B --> E[Next.js Frontend]
    B --> F[Timeline Canvas]
    B --> G[Preview Panel]

    E --> H[Zustand Stores]
    H --> H1[Editor State]
    H --> H2[Timeline State]
    H --> H3[Media State]
    H --> H4[Playback State]

    F --> I[Multi-track Timeline]
    I --> I1[Video Tracks]
    I --> I2[Audio Tracks]
    I --> I3[Overlay Tracks]

    G --> J[Real-time Preview]
    J --> K[DOM Rendering]
    J --> L[Binary Rendering Future]

    M[Storage System] --> N[IndexedDB]
    M --> O[OPFS File System]
    N --> P[Projects & Settings]
    O --> Q[Media Files]

    R[Processing] --> S[FFmpeg.js]
    R --> T[Background Removal]
    R --> U[Transcription]
```

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/en/) (v18 or later)
- [Bun](https://bun.sh/docs/installation) (npm alternative)
- [Docker](https://docs.docker.com/get-docker/) (optional, for database)

### Quick Setup

```bash
# 1. Fork and clone the repository
git clone https://github.com/YOUR_USERNAME/OpenCut.git
cd OpenCut

# 2. Navigate to web app
cd apps/web

# 3. Copy environment variables
cp .env.example .env.local

# 4. Install dependencies
bun install

# 5. Start development server
bun dev
```

### Environment Variables

```bash
# Database (matches docker-compose.yaml)
DATABASE_URL="postgresql://opencut:opencutthegoat@localhost:5432/opencut"

# Authentication
BETTER_AUTH_SECRET="your-generated-secret-here"
BETTER_AUTH_URL="http://localhost:3000"

# Redis
UPSTASH_REDIS_REST_URL="http://localhost:8079"
UPSTASH_REDIS_REST_TOKEN="example_token"
```

### Docker Development

```bash
# Start database and Redis services
docker-compose up -d

# Run database migrations
bun run db:migrate

# Start development server
bun run dev
```

## 📁 Project Structure

```
apps/
├── web/               # Main Next.js application
├── desktop/           # Tauri desktop app
├── bg-remover/        # Python background removal
└── transcription/     # Audio transcription service

src/
├── components/        # React components
├── stores/           # Zustand state management
├── hooks/            # Custom React hooks
├── lib/              # Utilities and services
└── types/            # TypeScript definitions
```

## 🎬 Video Editing Workflow

```mermaid
sequenceDiagram
    participant User
    participant Timeline
    participant Preview
    participant Storage
    participant FFmpeg

    User->>+Timeline: Import Media
    Timeline->>+Storage: Store in OPFS
    Storage-->>-Timeline: File Reference

    User->>+Timeline: Add to Track
    Timeline->>+Preview: Update Preview
    Preview-->>-User: Real-time Feedback

    User->>+Timeline: Apply Effects
    Timeline->>+Preview: Render Changes
    Preview-->>-User: Updated Preview

    User->>+Timeline: Export Video
    Timeline->>+FFmpeg: Process Timeline
    FFmpeg->>+Storage: Generate Output
    Storage-->>-User: Download Ready
```

## 🤝 Contributing

We welcome contributions! Focus areas include:

✅ **Recommended Areas:**
- Timeline functionality improvements
- Project management features
- Performance optimizations
- Bug fixes and UI improvements
- Documentation and testing

⚠️ **Avoid for Now:**
- Preview panel enhancements (undergoing refactor)
- Export functionality changes
- Preview rendering optimizations

### Quick Start for Contributors

```bash
# 1. Fork and clone
git clone https://github.com/YOUR_USERNAME/OpenCut.git

# 2. Create feature branch
git checkout -b feature/your-feature-name

# 3. Follow setup in CONTRIBUTING.md
# 4. Make changes and test
# 5. Submit pull request
```

## 🏢 Sponsors

Thanks to our sponsors for supporting open-source software:

[![Vercel](https://vercel.com/oss/program-badge.svg)](https://vercel.com/oss)
[![Powered by fal.ai](https://img.shields.io/badge/Powered%20by-fal.ai-000000?style=flat)](https://fal.ai)

## 📚 Resources

- [GitHub Repository](https://github.com/OpenCut-app/OpenCut)
- [Getting Started Guide](/docs/getting-started)
- [Development Setup](/docs/development)
- [Contributing Guide](/docs/contributing)
- [Security Policy](/docs/security)
- [Code of Conduct](/docs/code-of-conduct)

## 📄 License

[MIT License](https://github.com/OpenCut-app/OpenCut/blob/main/LICENSE) - Free for commercial and personal use.

---

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2FOpenCut-app%2FOpenCut&project-name=opencut&repository-name=opencut)
