# **@deno-kit/config**

[![JSR Score](https://jsr.io/badges/@deno-kit/config/score)](https://jsr.io/@deno-kit/config)
[![JSR](https://jsr.io/badges/@deno-kit/1.%20Clone%20this%20repository)](https://jsr.io/@deno-kit/config)
[![JSR Scope](https://jsr.io/badges/@deno-kit})](https://jsr.io/@deno-kit})
[![ci](https://github.com/zackiles/config/actions/workflows/ci.yml/badge.svg)](https://github.com/zackiles/config/actions/workflows/ci.yml)
[![license](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/zackiles/config/blob/main/LICENSE)

Combine dot-env, `Deno.env`, and general overrides into a simple unified global config module for your application.

> [!NOTE]
> This is a **new** project and the documentation is unlikely to be comprehensive or accurate.

## Usage

Import the `loadConfig` function from the module:

```typescript
import { loadConfig } from '@deno-kit/config' // Or the appropriate JSR/URL path

// Basic usage - returns default values if no env files exist
const config = await loadConfig()
console.log(config.DENO_ENV) // Access values like properties

// Load from custom env file if it exists
// Run your script like: deno run -A --config=prod.env script.ts
const configWithFile = await loadConfig()
console.log(configWithFile.CUSTOM_VAR) // Access values from prod.env

// With overrides - highest precedence but preserves other values
const configWithOverrides = await loadConfig({
  API_KEY: 'override-key', // Overrides any API_KEY from env files
  DATABASE_HOST: 'override-host', // Other env values are preserved
})
console.log(configWithOverrides.API_KEY) // Outputs: 'override-key'

// Using a custom logger
import { log } from '@std/log' // Example logger
const configWithLogger = await loadConfig(undefined, log)
```

See `src/lib.ts` JSDoc for more details on configuration sources and precedence.

## Features

- 🦖 **Modern Deno Features:** Built with the latest Deno runtime features.
- ⚙️ **Flexible Configuration:** Merges defaults, `Deno.env`, `.env` files, custom env files (via `--config` flag), and runtime overrides.
- 🔒 **Typed & Proxied:** Returns a strongly-typed proxy object for safe access and modification of config values (updates `Deno.env` automatically).
- 📝 **Customizable Logging:** Allows providing a custom logger instance.
- 📦 **Dynamic Value Resolution:** Supports asynchronous functions or Promises as default values.

## Development

```bash
# Run tests
deno task tests

# Format / lint / type-check code
deno task pre-publish
```

## **Changelog**

See the [`CHANGELOG`](CHANGELOG.md) for details.

## **Contributing**

See the [`CONTRIBUTING`](CONTRIBUTING.md) for details.

## **License**

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT) — see the [`LICENSE`](LICENSE) for details.
