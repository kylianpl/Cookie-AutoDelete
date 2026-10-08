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
- Release CI builds an XPI and attaches it to a GitHub Release (no store uploads,
  since this fork does not own the upstream AMO/Chrome listings).

## Build

```bash
npm ci
npm run build      # -> builds/Cookie-AutoDelete_*_Firefox.xpi (+ Chrome zip)
```

## Install the Firefox XPI

The XPI produced by this fork is **unsigned**, so on stable Firefox/Fennec you
must either:

- run **Firefox Nightly** (allows unsigned add-ons), or
- load it as a **temporary add-on** over USB remote debugging, e.g.:

  ```bash
  npm i -g web-ext
  web-ext run --source-dir=extension \
    --target=firefox-android --adb-device=<serial> \
    --firefox-apk=org.mozilla.fennec_fdroid --no-reload
  ```
- or sign it with your own AMO account (see “Extension ID” below).

## Extension ID

This fork currently keeps the upstream ID `CookieAutoDelete@kennydo.com`, which
means it can **not** be signed/installed permanently on stable Firefox — that ID
belongs to the upstream AMO listing. If you want a permanently installable,
AMO-signed build, change the ID (`applications.gecko.id` in
`extension/manifest.json`) to your own and sign it as a new unlisted add-on.

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
