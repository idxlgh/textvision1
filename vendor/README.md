# vendor

`anthropic-sdk.min.js` is the official Anthropic TypeScript/JavaScript SDK (`@anthropic-ai/sdk` 0.129.0, MIT License) bundled into a single classic script so `index.html` works without a build step — including when it is opened straight from disk (`file://`), where ES module imports are blocked. The bundle sets `window.Anthropic`.

To rebuild it (for example, to update the SDK version):

```bash
mkdir sdk-build && cd sdk-build
npm init -y && npm install @anthropic-ai/sdk@0.129.0 esbuild
printf 'import Anthropic from "@anthropic-ai/sdk";\nglobalThis.Anthropic = Anthropic;\n' > entry.mjs
npx esbuild entry.mjs --bundle --format=iife --platform=browser --target=es2020 --minify \
  --legal-comments=eof \
  "--banner:js=/*! @anthropic-ai/sdk 0.129.0 | MIT License | Copyright Anthropic, PBC | bundled for browser use: see vendor/README.md */" \
  --outfile=../vendor/anthropic-sdk.min.js
```
