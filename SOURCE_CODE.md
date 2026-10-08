# Source code & build instructions (for AMO reviewers)

This extension is built with **webpack** (which bundles and minifies the
sources), so a source code package is required. This archive contains the full
original source and everything needed to reproduce the submitted build.

## Environment

- **Node.js 20.x** (LTS) and **npm** (comes with Node).
- No native modules, no secret/private dependencies.

## Build

```bash
npm ci
npm run build
```

`npm run build` does two things:

1. **webpack** (config: `webpack.config.js`) compiles the TypeScript/React
   sources under `src/` into `extension/bundles/*.bundle.js`.
2. **tools/buildFilesDev.js** copies the static assets and packages the
   `extension/` folder into
   `builds/Cookie-AutoDelete_<version>_Firefox.xpi` (and a Chrome zip).

## Reproducing the submitted XPI

The submitted XPI is the output of the commands above on this source at version
`3.9.3`. `npm ci` installs the exact dependency tree pinned in
`package-lock.json`, so the build is reproducible with the Node version above.

## Project layout

- `src/` — TypeScript/React sources (background script, services, redux, UI).
- `extension/` — manifest, locales, icons, static HTML and the built `bundles/`.
- `webpack.config.js`, `tsconfig.json`, `tools/` — build tooling.
- `__tests__/` — Jest unit tests (`npm test`).

## Notes

This is a community fork of Cookie AutoDelete. Its main change is enabling the
site-data (LocalStorage, IndexedDB, cache, Service Workers) cleanup on Firefox
for Android (based on upstream PR #1803). See `FORK.md`.
