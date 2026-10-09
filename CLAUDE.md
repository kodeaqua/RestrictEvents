# RestrictEvents

Lilu plugin (macOS kernel extension, C++) that blocks problematic processes and patches
system UI/sysctls for unsupported hardware. See README.md for boot arguments.

## Layout
- `RestrictEvents/RestrictEvents.cpp` – plugin config, boot-arg/NVRAM parsing, TrustedBSD exec policy, userspace page patching (`cs_validate_*` hooks).
- `RestrictEvents/SoftwareUpdate.cpp/.hpp` – `kern.hv_vmm_present` and `hw.optional.f16c` sysctl hooks; private sysctl struct definitions.
- `RestrictEvents/vnode_types.hpp` – private XNU pager types (pre-Sierra).
- `Changelog.md` – update with every version bump (version lives in `MODULE_VERSION` in the xcodeproj).

## Build
Needs `Lilu.kext` (Debug build) and `MacKernelSDK` in the repo root (both git-ignored; symlinks are fine):

    ln -s ../MacKernelSDK MacKernelSDK
    ln -s ../Lilu/build/Debug/Lilu.kext Lilu.kext
    xcodebuild -jobs 4 -configuration Debug   # or Release

CI also runs `xcodebuild analyze`; keep it free of analyzer findings.

## Conventions
- Tabs for indentation; log tag `"rev"` (`"supd"` in SoftwareUpdate.cpp).
- Kernel context: no exceptions/RTTI, no libc heap assumptions, keep patches version-gated via `getKernelVersion()`.
- Commits: English, Conventional style (`feat:`/`fix:`/`chore:`).
- Cannot be loaded/tested in userspace; verify by building and reasoning carefully.
