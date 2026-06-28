# Honor 7X Kernel - SukiSU Edition

Honor 7X (BND-AL10) kernel source with modifications.

## Device Info
- **Device**: Honor 7X
- **SoC**: HiSilicon Kirin 659 (hi6250)
- **Kernel**: 4.9.148
- **Architecture**: ARM64

## Modifications

### 1. SELinux Permissive
- `CONFIG_SECURITY_SELINUX_DEVELOP=y` — enables runtime permissive/enforcing toggle
- `CONFIG_SECURITY_SELINUX_BOOTPARAM=y` — boot parameter control
- `CONFIG_SECURITY_SELINUX_DISABLE=y` — allows disabling SELinux
- SELinux defaults to **permissive** mode (selinux_enforcing=0)

### 2. Full BPF Support
- `CONFIG_BPF_JIT=y` — BPF JIT compiler
- `CONFIG_BPF_JIT_ALWAYS_ON=y` — always-on JIT, removes interpreter
- `CONFIG_NET_CLS_BPF=y` — BPF-based packet classifier
- `CONFIG_NET_ACT_BPF=y` — BPF-based packet actions
- Existing: `CONFIG_BPF`, `CONFIG_BPF_SYSCALL`, `CONFIG_CGROUP_BPF`

### 3. SukiSU Integration
- SukiSU-Ultra (KernelSU fork) integrated as `KernelSU/`
- Symlink: `drivers/kernelsu` → `KernelSU/kernel`
- `CONFIG_KSU=y` — KernelSU core
- `CONFIG_KPM=y` — SukiSU KPM (Kernel Patch Module) support
- `CONFIG_KPROBES=y` — required for kprobe-based hooking

## Build

GitHub Actions builds automatically on push to `main`.

Manual build:
```bash
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- merge_hi6250_defconfig
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc) Image.gz-dtb
```

## Source
Original kernel source from [Huawei Open Source](https://consumer.huawei.com/en/opensource/).

## License
See `COPYING` for license information.
