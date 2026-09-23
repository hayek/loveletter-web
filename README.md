<p align="center">
  <img src=".github/assets/icon.png" width="128" height="128" alt="Love Letter icon">
</p>

# loveletter-web

[![CI](https://github.com/hayek/loveletter-web/actions/workflows/ci.yml/badge.svg)](https://github.com/hayek/loveletter-web/actions/workflows/ci.yml) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

The **Web (TypeScript)** SDK in the [Love Letter](https://hayek.github.io/loveletter-docs/) family. It turns in-app feedback into a GitHub issue — in the exact same byte-for-byte wire format as the [Apple](https://github.com/hayek/LoveLetterSDK) and [Android](https://github.com/hayek/loveletter-android) SDKs.

> **Status:** all four packages build, typecheck, and pass their suites (including the cross-platform conformance gate). npm publishing is in progress — until then, install from this workspace.

## Packages

| Package | Purpose |
| --- | --- |
| `@loveletter/core` | Framework-agnostic: wire format + `RelayTransport` / `DirectGitHubTransport` |
| `@loveletter/widget` | Drop-in, dependency-free feedback form (`mountFeedbackWidget`) |
| `@loveletter/react` | `<FeedbackForm>` React wrapper |
| `@loveletter/relay` | The server-side handler **you** deploy (Cloudflare / Firebase / Appwrite / generic fetch) |

## The web is different: you host the relay

A browser can't safely hold a writable GitHub token — anything in client JS is public. So on the web the default path is a **relay you deploy and whose token you hold**; the browser only ever talks to your endpoint. The SDK ships reference relay handlers, but you run them. See the [security model](https://hayek.github.io/loveletter-docs/guides/security/) and [relay guide](https://hayek.github.io/loveletter-docs/guides/relay/).

```ts
import { mountFeedbackWidget } from '@loveletter/widget'
import { RelayTransport } from '@loveletter/core'

mountFeedbackWidget(el, {
  transport: new RelayTransport({ endpoint: '/api/feedback' }),
  appName: 'Acme',
  appVersion: '1.0.0',
})
```

A direct-to-GitHub transport exists for internal tools and prototypes, gated behind an explicit `dangerouslyUseClientToken` flag — it throws without it.

## Why byte-exact?

Every Love Letter SDK emits an identical GitHub issue body, pinned by a shared spec and a golden-fixture conformance suite ([`loveletter-spec`](https://github.com/hayek/loveletter-spec)) that runs in this repo's CI.

## Develop

```sh
corepack enable
pnpm install
pnpm -r test        # vitest, incl. the conformance gate in @loveletter/core
pnpm -r typecheck
```

API reference: <https://hayek.github.io/loveletter-docs/reference/typescript/>

## License

MIT © Amir Hayek. See [LICENSE](./LICENSE).
