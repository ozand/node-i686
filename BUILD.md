# Build instructions — Node.js v22.19.0 for i686

How to reproduce these builds on a 32-bit x86 Debian system.

## System requirements

| Component | Version used |
|-----------|-------------|
| OS | Debian 12 bookworm (i686) |
| Kernel | 6.1.0-686-pae |
| GCC | 12.2.0 (Debian 12.2.0-14+deb12u1) |
| Python | 3.11.2 |
| RAM | 2 GB (minimum; swap recommended) |
| Disk | ~5 GB free in build dir |
| Time | ~35 hours at `-j1` |

## Prerequisites

```bash
sudo apt install build-essential python3 git curl
```

## Download source

```bash
cd ~/build
wget https://nodejs.org/dist/v22.19.0/node-v22.19.0.tar.gz
tar xzf node-v22.19.0.tar.gz
cd node-v22.19.0
```

## Build variants

### `without-intl` — no Unicode property escapes (faster build, smaller binary)

```bash
./configure --openssl-no-asm --without-intl --dest-cpu=ia32 --prefix=/home/ozand/local
make -j1 2>&1 | tee build.log
make install
```

> ⚠️ `\p{...}` regex not supported. Tools like Pi CLI will not work.

### `small-icu` — with Unicode support (recommended)

```bash
./configure --openssl-no-asm --with-intl=small-icu --dest-cpu=ia32 --prefix=/home/ozand/local2
make -j1 2>&1 | tee build_smallicu.log
make install
```

> ✅ `\p{...}` regex works. Pi CLI and other modern tools work correctly.

## Notes on i686 compilation

- Use `-j1` (not `-j2` or higher) to avoid OOM kills on 2GB RAM
- `--openssl-no-asm` is required — the ASM optimizations fail on old i686 chips
- Official Node.js binaries do not support i686 — only x64, arm64, armv7
- V8 compilation (the heaviest part) takes ~20–25 hours of the total time
- Run inside `screen` or `nohup` — do not rely on SSH session staying open

## Verify binary

```bash
node --version        # v22.19.0
node -e "console.log(process.versions.icu)"  # e.g. 75.1 (small-icu build)
```
