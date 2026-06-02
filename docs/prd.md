# WordWise — PRD

## Overview
WordWise is a lightweight writing utility: paste text and instantly see word
count, character count, sentence count, and estimated reading time. It's a
standalone FastAPI app, adopted onto ShellAgent via the **external agent** path.

## Goals
- Instant, server-side text analysis behind a clean single-page UI.
- Zero external dependencies or API keys — works the moment it's deployed.

## Non-goals
- Grammar/spell checking, persistence, or user accounts.

## Users & use cases
Writers and editors who want a fast word-count + reading-time check before
publishing.

## Functional requirements
- `GET /` serves the UI.
- `POST /run` accepts `{ "input": "<text>" }` and returns `words`,
  `characters`, `characters_no_spaces`, `sentences`, `reading_time_minutes`,
  and a human `reading_time` string.
- `GET /health` returns `{ "status": "ok" }`.

## Technical requirements
- Python 3.11+, FastAPI + uvicorn, started via PM2 (`ecosystem.config.js`).
- Reading time = words ÷ 200 wpm.
- All UI assets are inlined so the page renders correctly behind a
  path-stripping reverse proxy.

## Acceptance criteria
- Health probe returns HTTP 200.
- Pasting text and clicking **Analyze** shows correct counts and reading time.
