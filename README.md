# OnePlus 9 Pro Android Common Kernel 6.18 manifest

This manifest syncs the source tree for the OnePlus 9 Pro (`lemonadep`,
SM8350/Lahaina) forward-port onto Android Common Kernel `android17-6.18`.

The tree follows the split used by the Lahaina/Yupik 6.18 reference port:

| Path | Repository | Contents |
|---|---|---|
| `kernel/lemonadep-6.18` | [lemonadep-6.18-kernel](https://github.com/blahajcoding/lemonadep-6.18-kernel) | ACK 6.18 plus the Qualcomm Lahaina platform and lemonadep kernel configuration |
| `kernel/lemonadep-6.18-modules` | [lemonadep-6.18-modules](https://github.com/blahajcoding/lemonadep-6.18-modules) | Qualcomm vendor modules and lemonadep board modules |
| `kernel/lemonadep-6.18-devicetrees` | [lemonadep-6.18-devicetrees](https://github.com/blahajcoding/lemonadep-6.18-devicetrees) | Lahaina base DT and lemonadep overlay/devicetree sources |

## Sync

```bash
repo init -u https://github.com/blahajcoding/android_kernel_manifest.git -b android17-6.18-lemonadep
repo sync --force-sync --no-clone-bundle --current-branch --no-tags -j$(nproc --all)
```

## Build

```bash
cd kernel/lemonadep-6.18
./build.sh
```

The build script uses the sibling module and devicetree checkouts when they
are present, downloads a pinned Android Clang/Rust toolchain, and writes output
to `out/lemonadep-6.18/dist` at the top of the repo workspace.

This is a forward-port: new work is implemented on ACK 6.18. The old SM8350
5.4 kernel and stock OPLUS module repositories are references only, not merge
bases.
