# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A minimal Node.js/Express tutorial reference project. A single `server.js` file serves as the entire application — there is no build step, no test suite, and no directory structure beyond the root.

## Commands

```bash
# Install dependencies
npm install

# Start the server (runs on port 8000)
npm start
# or
node server.js
```

There is no configured test runner (`npm test` exits with an error by default).

## Architecture

Everything lives in `server.js`. The app uses `body-parser` to parse JSON request bodies and defines three routes:

| Method | Path         | Description                                      |
|--------|--------------|--------------------------------------------------|
| GET    | `/users`     | Returns a hardcoded `mockUserData` array         |
| GET    | `/users/:id` | Echoes back the `:id` path param                 |
| POST   | `/login`     | Checks `username`/`password` against hardcoded mock credentials; returns a placeholder token string on match |

All data is in-memory mock data — there is no database or external service.

## Key Conventions

- Route handlers use `res.json()` with a consistent shape: `{ success: boolean, message: string, ...payload }`.
- `body-parser` is wired up globally via `app.use(bodyParser.json())`, so all POST bodies are parsed as JSON.
- The server binds to port `8000`.
- `express` is the only runtime dependency; `body-parser` is listed as a dependency in `package-lock.json` but not in `package.json` (it ships bundled with Express 4.x).
