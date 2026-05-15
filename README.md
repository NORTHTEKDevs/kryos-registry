# Kryos Package Registry

Official package index for the [Kryos programming language](https://github.com/NORTHTEKDevs/kryos-lang).

## Layout

Packages are stored as JSON files under a 2-char prefix derived from the package
name's first two characters:

```
<aa-zz>/<package-name>.json
```

For example, `json` -> `js/json.json`.

## Index entry schema

```json
{
  "name": "json",
  "description": "JSON parser and serializer",
  "homepage": "https://github.com/...",
  "license": "MIT",
  "versions": [
    {
      "version": "0.1.0",
      "git": "github:org/repo",
      "rev": "abc123...",
      "checksum": "sha256:...",
      "kryos": ">=1.2.0",
      "deps": {},
      "yanked": false
    }
  ]
}
```

## Publishing

```bash
kryos pkg publish
```

This is automated by the `kryos pkg publish` subcommand against
`https://github.com/NORTHTEKDevs/kryos-registry`.
