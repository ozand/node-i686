# node-i686

Node.js v22.19.0 compiled from source for **i686/x86 32-bit Linux** (Debian 12 bookworm).

Official Node.js does not provide i686 binaries. This repo preserves hand-compiled builds.

> **The binary is in [Releases →](https://github.com/ozand/node-i686/releases)**
> (GitHub stores large binaries in Releases, not in the file tree)

## Quick download

```bash
wget https://github.com/ozand/node-i686/releases/download/v22.19.0-i686-without-intl/node-v22.19.0-linux-i686-without-intl -O node
chmod +x node
./node --version  # v22.19.0
```

## Build info

| Field | Value |
|-------|-------|
| Node version | v22.19.0 |
| Arch | ia32 (i686) |
| OS | Debian 12 bookworm, kernel 6.1.0-686-pae |
| Build flags | `--openssl-no-asm --without-intl` |
| SHA256 | `2314405cea6ffc84282cf05080ed9107296e6d07c84ddaf48b8da5a628c97bdc` |
| Binary size | ~77 MB |

## Releases

| Tag | ICU | Notes |
|-----|-----|-------|
| [v22.19.0-i686-without-intl](https://github.com/ozand/node-i686/releases/tag/v22.19.0-i686-without-intl) | ❌ none | First working build; `\p{}` regex not supported |
| v22.19.0-i686-small-icu | ✅ small-icu | In progress — fixes Unicode property escapes for Pi CLI |

## Limitations of `without-intl` build

Built with `--without-intl`: V8 has no ICU data, so Unicode property escapes
(`\p{Letter}`, `\p{Control}`, etc.) in regex are not supported.
This breaks tools like [Pi coding agent](https://github.com/earendil-works/pi).

The `small-icu` build (currently compiling) will fix this.
