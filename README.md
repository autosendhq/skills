# Autosend Skill

Email API integration skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Send transactional emails, manage contacts, and use templates through the [autosendjs](https://www.npmjs.com/package/autosendjs) SDK.

## Prerequisites

- An [Autosend](https://autosend.com) account with a verified sending domain
- An API key (Settings > API Keys > Generate API Key)
- Environment variable set: `export AUTOSEND_API_KEY=as_your_key_here`

## Installation

```bash
npx skills add autosendhq/skills
```

## Quick Start

```bash
npm install autosendjs
```

```typescript
import { Autosend } from 'autosendjs';

const autosend = new Autosend(process.env.AUTOSEND_API_KEY);

await autosend.emails.send({
  from: { email: 'hello@yourdomain.com', name: 'Your Company' },
  to: { email: 'user@example.com', name: 'Test User' },
  subject: 'Hello from Autosend!',
  html: '<h1>It works!</h1><p>Your Autosend integration is ready.</p>',
});
```

## Features

- **Single email** — Send transactional emails with HTML and plain text support
- **Bulk send** — Send to multiple recipients with shared sender, subject, and optional per-recipient dynamic data
- **Templates** — Use pre-built templates with dynamic data (order confirmations, welcome emails, password resets, etc.)
- **Contact management** — Create, get, upsert, and delete contacts with custom fields and list assignments
- **TypeScript support** — Full type definitions for all SDK methods and options
- **Error handling** — Structured error codes (`UNAUTHORIZED`, `RATE_LIMIT_EXCEEDED`, `VALIDATION_FAILED`) for reliable integrations
- **Configurable SDK** — Custom timeouts, retries, debug logging, and base URL options

## Documentation

- [SKILL.md](SKILL.md) — Full skill documentation with detailed examples for every feature
- [API Guide](references/api-guide.md) — Autosend API overview and concepts
- [REST API Reference](references/rest-api.md) — Examples for Python, Go, Ruby, Rust, and curl

## License

MIT
