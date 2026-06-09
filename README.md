# openssl-windows

Mirror of [Shining Light Productions'](https://slproweb.com/products/Win32OpenSSL.html)
**Win64 OpenSSL** static MSVC installers, re-hosted as GitHub release assets.

## Why

slproweb deletes old point releases the moment a new one ships — the `3.6.2`
installer URL 404s as soon as `3.6.3` is published. That breaks any pinned fetch
(our Nix `fetchurl` of `Win64OpenSSL-<version>.msi`). Each release here serves the
**byte-identical** `.msi`, so the pinned SHA-256 is unchanged; only the URL moves
to a host that doesn't expire.

We need slproweb's build specifically: it is **static** (the launcher ships a single
`.exe`, no DLLs) and **keeps the deprecated OpenSSL 3.0 APIs** the `openssl` crate
uses (clamwin's static build is no-deprecated; FireDaemon's is dynamic). OpenSSL
itself can't be cross-built MSVC from Linux, so we extract the prebuilt static libs
(`libcrypto_static.lib` / `libssl_static.lib`) + headers from the installer.

## Layout

| | |
|---|---|
| Release tag | the OpenSSL version, e.g. `3.6.3` |
| Asset | `Win64OpenSSL-<version, `.`→`_`>.msi`, e.g. `Win64OpenSSL-3_6_3.msi` |

Consumed by `nix/packages/openssl-windows.nix` in
[w3champions/launcher-e](https://github.com/w3champions/launcher-e).

## License

OpenSSL 3.x is licensed under the [Apache License 2.0](https://www.openssl.org/source/license.html).
Redistribution of the unmodified installer is permitted.
