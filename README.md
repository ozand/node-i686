# node-i686

Node.js v22.19.0 compiled from source for **i686/x86 32-bit Linux** (Debian 12 bookworm).

Official Node.js does not provide i686 binaries. This repo preserves hand-compiled builds.

## Download

See [Releases](https://github.com/ozand/node-i686/releases).

## Build info

| Field | Value |
|-------|-------|
| Node version | v22.19.0 |
| Arch | ia32 (i686) |
| OS | Debian 12 bookworm |
| Build flags | `--openssl-no-asm --without-intl` |
| SHA256 | `2314405cea6ffc84282cf05080ed9107296e6d07c84ddaf48b8da5a628c97bdc` |

## Limitations

Built with `--without-intl`: Unicode property escapes (`\p{...}`) in regex are not supported.
A rebuild with `--with-intl=small-icu` is in progress.

## Usage

```bash
wget https://github.com/ozand/node-i686/releases/download/v22.19.0-i686-without-intl/node-v22.19.0-linux-i686-without-intl -O node
chmod +x node
./node --version  # v22.19.0
```
