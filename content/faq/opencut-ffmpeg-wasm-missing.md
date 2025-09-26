+++
title = "Fix Missing @ffmpeg/ffmpeg Wasm in OpenCut"
description = "Resolve @ffmpeg/ffmpeg wasm loading failures inside the OpenCut editor."
draft = false
+++

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "@id": "https://opencut.dev/faq/opencut-ffmpeg-wasm-missing",
    "name": "How do I fix ffmpeg.wasm missing errors in OpenCut?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Ensure @ffmpeg/ffmpeg is installed, mark ffmpeg-core.js and ffmpeg-core.wasm as static assets in next.config.mjs, and call createFFmpeg({ log: true, corePath }) with the correct CDN or local path."
    }
  }]
}
</script>

If the editor logs `Failed to load ffmpeg-core.wasm`, the bundle cannot find the WASM core.

## Checklist
1. Install the package:
   ```bash
   bun add @ffmpeg/ffmpeg @ffmpeg/core
   ```
2. Configure static file serving in `next.config.mjs`:
   ```js
   const withTM = require('next-transpile-modules')(['@ffmpeg/ffmpeg', '@ffmpeg/core']);
   module.exports = withTM({
     webpack: (config) => {
       config.experiments = { ...config.experiments, asyncWebAssembly: true };
       return config;
     }
   });
   ```
3. Reference the core explicitly:
   ```ts
   const ffmpeg = createFFmpeg({
     log: true,
     corePath: '/static/ffmpeg/ffmpeg-core.js'
   });
   ```
4. Copy assets during build (e.g., using `next.config.mjs` `rewrites` or a build script).

## Diagram

```mermaid
flowchart LR
    A[createFFmpeg] --> B[ffmpeg-core.js]
    B --> C[ffmpeg-core.wasm]
    C --> D[Browser]
```

Host the WASM on a CDN like jsDelivr if you deploy to serverless targets that cannot serve large static files from the filesystem.
