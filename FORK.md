# Cookie-AutoDelete — maintained fork

This repository is a **community-maintained fork** of
[Cookie-AutoDelete](https://github.com/Cookie-AutoDelete/Cookie-AutoDelete).

Upstream is effectively unmaintained: the last *release* is **v3.8.2 (2022-12-08)**
and, since then, only dependency/CI bumps have landed. Two long-standing PRs are
still open upstream:

- **#1803 — “Let Firefox on Android manage all storage types”** (the fix this fork
  is built on): since Firefox for Android is GeckoView-based, the site-data
  cleanup APIs (`browsingData.remove()`) are available, but upstream still
  force-disables the site-data settings and skips the cleanup on Android. Result:
  cookies were cleaned on Android while **LocalStorage / IndexedDB / cache /
  Service Workers were left behind**.
- #1735 — “Migrate to MV3 and Modern Redux” (large, not merged upstream).

## Branch layout

| Branch | Purpose |
| --- | --- |
| `3.X.X-Branch` | Read-only mirror of `upstream/3.X.X-Branch` (default upstream branch). |
| `main` | Fork integration branch: `upstream/3.X.X-Branch` + curated fixes (currently PR #1803). |

To sync with upstream:

```bash
git fetch upstream
git checkout main
git merge upstream/3.X.X-Branch
```

## What this fork changes

- Carries the Android site-data fix (equivalent to upstream PR #1803), with
  attribution to its author.
- Rebranded as **CAD Neo** (name, description, homepage and a recoloured logo)
  so it is clearly a fork and does not conflict with the upstream AMO listing.
- Has its own extension ID `CAD-Neo@kytech.fr`, allowing AMO to sign it.
- Release CI builds the XPI, signs it with AMO and attaches it to a GitHub
  Release, and submits a **listed** version to AMO so it can be installed from
  the AMO page (required for Firefox for Android).

See `AMO_LISTING.md` for the text used on the AMO listing.

## Build

```bash
npm ci
npm run build      # -> builds/Cookie-AutoDelete_*_Firefox.xpi (+ Chrome zip)
```

## Install

- **Firefox for Android**: install **CAD Neo** from its AMO page (listed).
  Firefox for Android only installs extensions from AMO, so the listed channel
  is required.
- **Desktop**: install from AMO, or use the AMO-signed XPI from `builds/amo/`
  via `about:addons` → “Install Add-on From File”.
- The `Cookie-AutoDelete_*_Firefox.xpi` release asset is the **unsigned** build,
  for Firefox Nightly / temporary add-on development.

## Extension ID & signing

This fork uses its own ID `CAD-Neo@kytech.fr`
(`applications.gecko.id` in `extension/manifest.json`), independent from the
upstream AMO listing.

CI signs with `web-ext sign`:

- `--channel=unlisted` → signed XPI attached to the GitHub Release;
- `--channel=listed` → submits the version to the public AMO listing (best
  effort; the version may go through review).

Add these repository secrets (Settings → Secrets and variables → Actions):

- `WEB_EXT_API_KEY`
- `WEB_EXT_API_SECRET`

(AMO → Tools → “Manage API keys”.)

## Releases

Push a semver tag and CI builds + publishes:

```bash
git tag v3.9.0
git push origin v3.9.0
```

## Credits

All original work by the Cookie-AutoDelete team
(https://github.com/Cookie-AutoDelete/Cookie-AutoDelete/graphs/contributors).
Android storage support by @mlindsay (upstream PR #1803). Licensed MIT.
