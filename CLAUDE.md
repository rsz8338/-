# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A minimal Node.js/Express web app that displays haikus paired with images. Originally built as a GitHub Codespaces demo template, based on the Azure App Service hello-world sample. There are no tests.

## Commands

```bash
npm install        # install dependencies
npm start          # start server (node index.js) on PORT env var or 3000
npm run dev        # start with nodemon (auto-restarts on file changes)
```

## Architecture

The app has a single route (`GET /`) in `index.js` that renders `views/index.ejs`, passing all haiku data loaded at startup from `haikus.json`.

- **`haikus.json`** — data file; each entry has a `text` (newline-separated haiku string) and an `image` (filename relative to `public/images/`)
- **`views/index.ejs`** — the only template; iterates over haikus and renders each with its image
- **`public/`** — static assets served directly by Express (`express.static`)
- **`process.json`** — PM2 process config (watches for changes via polling)
- **`web.config`** — IIS/iisnode config for Azure App Service deployment; maps static requests to `public/` and all other requests to `index.js`

To add a new haiku, add an entry to `haikus.json` and place the corresponding image in `public/images/`.
