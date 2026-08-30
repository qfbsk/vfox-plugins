# vfox-plugins (custom registry)

A custom [vfox](https://vfox.dev) plugin registry, structured exactly like the official
`version-fox/vfox-plugins` index. Point QfPlus / vfox at this repo:

```
vfox config registry.address <this-repo-url>
```

or, in QfPlus, set the "GitHub 源 / registry" field to this repo's address.

## How it is organized (mirrors the official design)

- `plugins/<name>.json`  — a pointer to a plugin's release zip (name, version, downloadUrl, license...).
- `sources/<name>.json`  — the plugin manifest address + a smoke-test used by the registry bot.

This repo stores **only JSON pointers**. It never contains plugin code or SDK binaries.
Every plugin lives in **its own repository**; this index just tells vfox where to find them.

## What it points to

- `plugins/mingw.json`  → our own MinGW plugin repo (`vfox-mingw`)
- `plugins/nodejs.json` → the official nodejs plugin repo (example of aggregating an external lib)

## Add your own plugin

1. Create a plugin repo (see `vfox-mingw` for a working template).
2. Publish a release zip, e.g. `vfox-foo-0.1.0.zip`.
3. Add `plugins/foo.json` (and optionally `sources/foo.json`) here pointing at that release.
4. Commit & push. Users then get it with `vfox add foo`.
