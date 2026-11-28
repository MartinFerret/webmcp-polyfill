# Next.js

## Load the polyfill

In Next.js 15.3+, add this to `instrumentation-client.ts` beside `app` (or `src/instrumentation-client.ts` beside `src/app`):

```ts
import "@w3c/webmcp-polyfill/auto";
```

Next.js runs [client instrumentation](https://nextjs.org/docs/app/api-reference/file-conventions/instrumentation-client) before hydration. A Server Component import alone won't install the polyfill in the browser.

Both entry points, `@w3c/webmcp-polyfill/auto` and `installWebMCP()`, are SSR-safe: installation does nothing without a document. Your pages can stay server-rendered; WebMCP runs in the browser.

## Register a tool

The package needs no `"use client"` directive. Use it on your [Client Components](https://nextjs.org/docs/app/api-reference/directives/use-client) and access `document.modelContext` in effects or event handlers. Pass an `AbortSignal` when registering in an effect, then abort it during cleanup.
