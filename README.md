# Kryos Package Registry

Official registry for the [Kryos](https://github.com/NORTHTEKDevs/kryos-lang) language.

## Index format

Packages are indexed under `<first-two-chars>/<name>.json` with one newline-delimited
JSON entry per version. Tarballs are hosted as GitHub Releases on this repo,
tagged as `<package>-v<version>`.

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

Open a PR adding a `<prefix2>/<name>.json` entry and create a release with the tarball asset
tagged as `<package>-v<version>`.

## Layout

```
<aa-zz>/<package-name>.json
```

For example, `markdown` → `ma/markdown.json`, `http-router` → `ht/http-router.json`.
