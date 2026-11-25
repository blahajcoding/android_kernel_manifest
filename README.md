# lemonadep 6.18 kernel manifest

Repo manifest for the forward-port of the **OnePlus 9 Pro** (`lemonadep`,
SM8350/Lahaina) to Android Common Kernel 6.18.

## Sync

```bash
repo init -u https://github.com/blahajcoding/android_kernel_manifest.git -b lemonadep-6.18
repo sync --force-sync --no-clone-bundle --current-branch --no-tags -j"$(nproc --all)"
```

The manifest intentionally contains only the three source repositories needed
by the 6.18 build:

- `kernel/lemonadep-6.18` — ACK 6.18 kernel, build system and integration metadata
- `kernel/lemonadep-6.18-modules` — Qualcomm/vendor module sources and build scripts
- `kernel/lemonadep-6.18-devicetrees` — Lahaina base and lemonadep overlay devicetrees

Unlike the old 5.4 manifest, no AOSP `kernel/build` checkout or host prebuilts
are required. The kernel's `build.sh` pins and downloads its own toolchain
(Android Clang r596125, Rust, bindgen, pahole, mkdtboimg and AnyKernel3).

## Build

```bash
cd kernel/lemonadep-6.18
./build.sh          # tools, kernel, modules, dtbo and AnyKernel3 zip
```

Useful partial steps:

```bash
./build.sh kernel   # baseline kernel Image and in-tree modules
./build.sh modules  # vendor/out-of-tree modules
./build.sh dtbo     # lemonadep normal + T0 dtbo image
./build.sh zip      # flashable AnyKernel3 package
```

## Status

This is an active forward-port, not a complete hardware enablement release.
Read `PORTING.md` in the kernel repository before flashing. In particular,
display, touch, camera sensors, audio amps, charging, NFC, fingerprint and
several other device-specific blocks are explicitly deferred or under active
migration; they are not silently stubbed out.
