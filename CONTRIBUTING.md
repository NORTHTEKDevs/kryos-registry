# Contributing to kryos-registry

This repository is the canonical package index for Kryos. Publishing or
yanking a package is a Pull Request against this repo. There is no upload
API.

## Publishing a new package version

1. **Pack your package** from your source repo:

   ```
   kryos pkg pack
   ```

   This produces `target/package/<name>-<version>.tar.gz` and prints a
   JSON index entry to stdout (`sha256:<64-hex>` checksum of the
   tarball bytes).

2. **Upload the tarball** to this repo under `tarballs/<name>-<version>.tar.gz`.

3. **Open a PR against this repository:**
   - Compute the prefix directory: first two characters of the package
     name, lowercase. For single-character names, the prefix is the
     whole name.
   - Append the generated JSON line to `<prefix>/<name>.json`. Create
     the file if it doesn't exist.
   - The JSON line must conform to the canonical schema:
     ```json
     {"name": "...", "version": "...", "dependencies": {}, "checksum": "sha256:<64-hex>", "download_url": "..."}
     ```
   - Set `download_url` to
     `https://raw.githubusercontent.com/NORTHTEKDevs/kryos-registry/master/tarballs/<name>-<version>.tar.gz`.
   - Optionally tag a GitHub Release as `<name>-v<version>` for a
     secondary discoverability marker.

4. **CI validates** every PR. Required fields: `name`, `version`,
   `dependencies` (must be a JSON object, possibly empty), `checksum`
   (must match `sha256:<64-hex>`), `download_url` (must be HTTPS).
   The `name` field must match the filename, the prefix directory must
   match the name, and the `version` must be unique within the file.

5. **A maintainer reviews and merges.** Once merged, clients pick up
   the new version on their next `kryos pkg sync`.

## Yanking a version

Open a PR that adds `"yanked": true` to the appropriate JSON line.
Yanked versions stay in the index forever; clients warn when resolving
them and never auto-upgrade to a yanked version.

## Why PR-based?

Because immutability and audit trail are more valuable here than
convenience. The Git history of this repo is the audit log of every
publish, and human review is the only mechanism we have to catch
name-squatting and typosquatting.

## What's NOT allowed

- **Republishing a `(name, version)` tuple.** Once a version is in the
  index, its tarball bytes are immutable. To fix a bad release, yank it
  and publish a new version (typically the next patch).
- **Editing a `download_url` to point at different bytes.** This breaks
  the checksum guarantee and is treated as a security incident.
- **Removing entries.** Yanking is the only way to deprecate.
