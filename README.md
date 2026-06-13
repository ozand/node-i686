# node-i686

Node.js v22.19.0 compiled from source for **i686/x86 32-bit Linux** (Debian 12 bookworm).

Official Node.js does not provide i686 binaries. This repo preserves hand-compiled builds.

> **The binaries are in [Releases →](https://github.com/ozand/node-i686/releases)**
> (GitHub stores large binaries in Releases, not in the file tree)

## Quick download — recommended build (small-icu)

```bash
wget https://github.com/ozand/node-i686/releases/download/v22.19.0-i686-small-icu/node-v22.19.0-linux-i686-small-icu -O node
chmod +x node
./node --version               # v22.19.0
./node -e "console.log(process.versions.icu)"  # 77.1
```

## Releases

| Tag | ICU | Binary size | SHA256 | Notes |
|-----|-----|-------------|--------|-------|
| [v22.19.0-i686-small-icu](https://github.com/ozand/node-i686/releases/tag/v22.19.0-i686-small-icu) | ✅ 77.1 | 86 MB | `8ee66d30684e9d01ae5667b23c3960d35084b628abe84b4f3c7daab559900d1b` | **Recommended** — Unicode regex `/v`, Pi CLI works |
| [v22.19.0-i686-without-intl](https://github.com/ozand/node-i686/releases/tag/v22.19.0-i686-without-intl) | ❌ none | 77 MB | `2314405cea6ffc84282cf05080ed9107296e6d07c84ddaf48b8da5a628c97bdc` | First build; `\p{}` regex not supported |

## Build flags

### small-icu (recommended)
```
./configure --openssl-no-asm --with-intl=small-icu --dest-cpu=ia32
```
- Supports Unicode property escapes (`\p{L}`, `\p{Emoji}`, etc.)
- Required for [Pi coding agent](https://github.com/earendil-works/pi)
- **Patch**: removed `ia32` from `deps/zlib/zlib.gyp` SIMD chunk conditions (fixes `_mm_set1_epi64x` 64-bit intrinsic error)

### without-intl (legacy)
```
./configure --openssl-no-asm --without-intl --dest-cpu=ia32
```
- No ICU data — Unicode property escapes not supported
- `process.versions.icu === undefined`

## Host info

| Field | Value |
|-------|-------|
| OS | Debian 12 bookworm |
| Kernel | 6.1.0-42-686-pae |
| Arch | i686 |
| Compiler | gcc 12 (i686-linux-gnu) |

## See also

- [BUILD.md](BUILD.md) — full build instructions and reproduce steps

