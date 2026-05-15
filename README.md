# Kryos Package Registry

Official registry for the [Kryos](https://github.com/NORTHTEKDevs/kryos-lang) language.

## Index format

Packages are indexed under `<first-two-chars>/<name>.json` with one newline-delimited
JSON entry per version. Tarballs are hosted inside this repo under `tarballs/` and
served via `raw.githubusercontent.com`. GitHub Release tags also exist as a
secondary marker (`<package>-v<version>`).

Each entry has the form:
```json
{"name": "...", "version": "...", "dependencies": {}, "checksum": "sha256:<HEX>", "download_url": "..."}
```

## Available packages

- `markdown` — CommonMark-subset Markdown to HTML renderer
- `http-router` — Simple HTTP request/response structs and routing helpers
- `json` — Friendly wrappers around Kryos built-in JSON functions
- `sqlite` — FFI wrapper for SQLite via libsqlite3
- `regex` — Regex matching (POSIX ERE via libc, with pure-Kryos fallback)

## Usage

```sh
kryos pkg sync
kryos pkg search markdown
kryos pkg add markdown
```

## Adding a package

Open a PR that:
1. Adds the package source as a `tarballs/<name>-<version>.tar.gz` archive
2. Adds a `<prefix2>/<name>.json` index entry with a `download_url` pointing at
   `https://raw.githubusercontent.com/NORTHTEKDevs/kryos-registry/master/tarballs/<name>-<version>.tar.gz`
3. Tags a release as `<package>-v<version>` (optional but recommended)

## Layout

```
<aa-zz>/<package-name>.json
```

For example, `markdown` → `ma/markdown.json`, `http-router` → `ht/http-router.json`.
