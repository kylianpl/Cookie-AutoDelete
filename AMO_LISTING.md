# AMO listing — CAD Neo

Copy/paste these into the AMO Developer Hub listing for `CAD-Neo@kytech.fr`.

## Name
```
CAD Neo
```

## Summary (short — from the manifest description)
```
Community fork of the unmaintained Cookie AutoDelete. Automatically clears cookies and site data (LocalStorage, IndexedDB, cache, service workers) from closed tabs, with full Firefox for Android support.
```

## Description (long)
```markdown
**CAD Neo** is a community-maintained fork of
[Cookie AutoDelete](https://github.com/Cookie-AutoDelete/Cookie-AutoDelete).

## Why this fork exists

Cookie AutoDelete has not had a release since **v3.8.2 (December 2022)**.
Since then the upstream project has only seen dependency and CI updates, and
long-standing pull requests — including full **Firefox for Android** support —
have not been merged or shipped.

As a result, on Firefox for Android the upstream extension cleans **cookies**
but silently leaves other site data behind: **LocalStorage, IndexedDB, the
cache and Service Workers**. That is easy to miss and defeats the point of the
extension on mobile.

## What CAD Neo changes

- **Full site-data cleanup on Firefox for Android**: the LocalStorage,
  IndexedDB, cache, plugin and Service Worker cleanup options are now available
  in Settings (and per expression) and actually run, instead of being hidden and
  skipped. Requires Firefox for Android 85+.
- Keeps the classic Cookie AutoDelete behaviour on desktop.
- Focused, small changes on top of upstream — no unrelated rewrites.

## What it does

- Deletes cookies from tabs you close, while keeping the sites you trust
  (whitelist / expressions).
- Optionally clears LocalStorage, IndexedDB, cache and Service Workers.
- Containers, cleanup log, manual cleaning, import/export of settings.

## Credits & license

All original work is by the Cookie AutoDelete team. Android site-data support
is based on upstream PR
[#1803](https://github.com/Cookie-AutoDelete/Cookie-AutoDelete/pull/1803) by
[@mlindsay](https://github.com/mlindsay). Licensed under MIT. The source is at
https://github.com/kylianpl/Cookie-AutoDelete.

This fork is **not affiliated with** the original authors; it exists to keep the
extension working, especially on Android.
```

## Homepage
```
https://github.com/kylianpl/Cookie-AutoDelete
```

## Support site
```
https://github.com/kylianpl/Cookie-AutoDelete/issues
```
