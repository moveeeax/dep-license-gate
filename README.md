# dep-license-gate

> The declared license field is a suggestion. Read the package.

**Status:** 🚧 In development

## Overview

Fail a build on dependency licenses outside an allow list, resolving the real license from package metadata instead of trusting a declared field.

## Features

- Resolves licenses from the package archive itself — LICENSE files, `go.mod` module paths, `PKG-INFO`, POM and npm metadata — and reports where each answer came from
- Flags the mismatch case explicitly: a manifest that says MIT over a bundled GPL file
- Normalizes to SPDX identifiers, including the common malformed spellings, and marks anything it could not resolve as unknown rather than silently allowing it
- Walks transitive dependencies, so a copyleft package four levels down is not missed
- Allow list, deny list and per-package exceptions with an expiry date, so a temporary waiver actually expires
- Consumes and emits SPDX and CycloneDX SBOMs, with a non-zero exit code and a diff against the previous run

## Stack

Go + google/licensecheck and go-license-detector for classification, cobra, and CycloneDX/SPDX Go libraries for SBOM I/O.

## Usage

```bash
dep-license-gate scan ./ --allow MIT,Apache-2.0,BSD-3-Clause \
  --deny AGPL-3.0 --fail-on-unknown --format sarif
```

## License

MIT

---

Archived on 2026-11-05. The idea moved to [sbom-action](https://github.com/moveeeax/sbom-action/issues/2).
