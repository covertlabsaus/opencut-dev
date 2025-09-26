+++
title = "Clear Bun Cache Issues in OpenCut"
description = "Reset Bun's module cache when OpenCut dependencies fail to resolve or mismatch."
draft = false
+++

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "@id": "https://opencut.dev/faq/opencut-bun-cache-issues",
    "name": "Why is Bun caching dependencies incorrectly in OpenCut and how do I clear it?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Delete ~/.bun/install/cache along with project node_modules and .turbo directories, then rerun bun install so the workspace rebuilds with clean metadata."
    }
  }]
}
</script>

Bun aggressively caches packages. When lockfiles change or a dependency publishes a bad build, clear the cache and reinstall.

## Cleanup script

```bash
rm -rf ~/.bun/install/cache
rm -rf node_modules .turbo .next
bun install
```

## Verify versions

```bash
bun pm ls react
bun pm ls @ffmpeg/ffmpeg
```

Ensure the package versions match `package.json`.

## Lockfile hygiene
- Commit `bun.lock` with dependency changes.
- Avoid mixing `npm install` and `bun install` in one branch.
- Run `bun pm dedupe` after large upgrades.

## Diagram

```mermaid
flowchart LR
    A[Cached metadata] --> B[Clear ~/.bun/install/cache]
    B --> C[Remove node_modules]
    C --> D[bun install]
    D --> E[Fresh dependency graph]
```

If the error persists, try `pnpm install` to isolate whether the upstream package is broken before returning to Bun.
