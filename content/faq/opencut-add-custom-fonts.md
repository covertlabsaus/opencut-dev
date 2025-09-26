+++
title = "Add Custom Fonts to the OpenCut Editor"
description = "Load custom font files into OpenCut's timeline canvas and preview panels."
draft = false
+++

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "@id": "https://opencut.dev/faq/opencut-add-custom-fonts",
    "name": "How do I add custom fonts to the OpenCut editor?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Copy fonts into apps/web/public/fonts, register @font-face rules, extend tailwind.config.ts, and preload the font in the editor font registry so both canvas and preview use it."
    }
  }]
}
</script>

OpenCut uses Tailwind and a shared font registry to render text consistently.

## Steps
1. Copy the font files:
   ```bash
   mkdir -p apps/web/public/fonts
   cp ~/Downloads/NeonStream.woff2 apps/web/public/fonts/neon-stream.woff2
   ```
2. Register in `tailwind.config.ts`:
   ```ts
   extend: {
     fontFamily: {
       neon: ['"NeonStream"', 'cursive']
     }
   }
   ```
3. Add an `@font-face` rule (`apps/web/styles/fonts.css`):
   ```css
   @font-face {
     font-family: 'NeonStream';
     src: url('/fonts/neon-stream.woff2') format('woff2');
     font-display: swap;
   }
   ```
4. Import the CSS in `_app.tsx` or `globals.css`:
   ```ts
   import '../styles/fonts.css';
   ```
5. Preload in the editor font registry (e.g., `apps/web/src/lib/fonts.ts`):
   ```ts
   fontRegistry.load('NeonStream', '/fonts/neon-stream.woff2');
   ```

## Diagram

```mermaid
flowchart TD
    A[public/fonts] --> B[@font-face]
    B --> C[Tailwind classes]
    C --> D[Timeline canvas]
```

Commit the font assets so deployments (Vercel, Docker) ship with identical typography.
