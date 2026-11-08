# KRNL OS releases

This repository holds the signed releases of KRNL OS, and nothing else: no source code. The code
lives in KRNL Studio's own repository, whose release workflows build, check and sign each release and
hand it here.

- **The desktop app**: releases tagged `app-vX.Y.Z`. The `.dmg` is one app for Macs with Apple
  silicon or Intel, signed with KRNL Studio's Developer ID and notarised by Apple. The `.deb` and the
  AppImage are for Linux on x86-64.
- **krnld**, the helper that runs agents on a machine: releases tagged `krnld-vX.Y.Z`, one archive for
  each of Linux and macOS on x86-64 and ARM.
- **`updates`**: the release that installed apps and krnlds read. It holds `app.json` and
  `krnld.json`, which name the newest release's files and their signatures.

An installed app or krnld takes an update only when it is signed by KRNL's release key, which each
build has built in, for the version it announces. The key's public half, as `tauri signer` writes it:

```
dW50cnVzdGVkIGNvbW1lbnQ6IG1pbmlzaWduIHB1YmxpYyBrZXk6IDBENUFEN0Q3MEY1OEI1NTYKUldSV3RWZ1AxOWRhRFJYVFdzUU04bzE4L2pFYW0xY2gvM3JCSStDNXNLU2JhY21rMWpYQ0QzT2UK
```

That is minisign key `0D5AD7D70F58B556`. A `.sig` file beside each update package is its signature.

Nothing is committed here by hand: the release workflows publish each release, and point `updates`
at it, once every package has been built, installed and opened on clean machines, and signed.
