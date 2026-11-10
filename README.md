# lava-artifacts

Kernel images, device trees and NFS rootfs archives for the LAVA health
checks of a private test lab. They cover the PREEMPT_RT builds that
[montjoie/lava-healthchecks-binary](https://github.com/montjoie/lava-healthchecks-binary)
doesn't have: it tracks mainline and stable kernels.

The files are assets of this repo's
[releases](https://github.com/igaw/lava-artifacts/releases), not git
objects, so a clone stays small and downloads need no Git LFS quota.

```
https://github.com/igaw/lava-artifacts/releases/download/<tag>/<file>
```

A release is never changed; something new is a new release. What a
release contains, which configs it was built with and what changed is
in its release notes. This README only describes the scheme.

## Releases

There are two kinds:

- **Kernel releases**, tagged with the linux-stable-rt version
  (`v<version>-rt<n>`): a kernel per board, and the device trees.
- **Rootfs releases**, tagged `rootfs-<yyyy.mm.dd>`: one NFS rootfs
  archive per architecture.

A job combines a kernel release with a rootfs release; the notes of a
kernel release say which rootfs it needs. (The oldest release,
`v4.19.325-rt140`, carries its own rootfs instead.)

Each release has a `SHA256SUMS` for its files. Rootfs releases also
have `BUILDINFO`: the kiwi-lava commit, the Tumbleweed snapshot per
architecture and the build date.

## File names

| Board | LAVA device type | Kernel | Device tree | Rootfs |
|---|---|---|---|---|
| c2d | `x86` (boots via iPXE) | `c2d-image-<variant>-<tag>` (bzImage) | none | `lava-image.x86_64-1.tar.xz` |
| bbb | `beaglebone-black` | `bbb-image-<variant>-<tag>` (zImage) | `am335x-boneblack.dtb` | `lava-image.armv7l-1.tar.xz` |
| rpi3-32 | `bcm2837-rpi-3-b-32` | `rpi3-32-image-<variant>-<tag>` (zImage) | `bcm2837-rpi-3-b-plus.dtb` | `lava-image.armv7l-1.tar.xz` |
| rpi3-64 | `bcm2837-rpi-3-b` | `rpi3-64-image-<variant>-<tag>` (Image) | `bcm2837-rpi-3-b-plus.dtb` | `lava-image.aarch64-1.tar.xz` |

`<variant>` is the preemption flavor of
[igaw/srt-build](https://github.com/igaw/srt-build): `rt` (PREEMPT_RT,
what the health checks boot), and in some releases also `up`, `ll`,
`vp`, `nohz` or `lazy`. A release doesn't have to cover every board.

rpi3-32 and rpi3-64 use the same device tree file. The rootfs archives
are for test boards only: root has an empty password.

## Sources

- Kernels: tags of
  [linux-stable-rt](https://git.kernel.org/pub/scm/linux/kernel/git/rt/linux-stable-rt.git),
  configs from [igaw/srt-build](https://github.com/igaw/srt-build)
  (`configs/`, `config.yml`); the release notes name the srt-build
  commit. For v4.19 it isn't recorded.
- Rootfs: [igaw/kiwi-lava](https://github.com/igaw/kiwi-lava), KIWI NG,
  openSUSE Tumbleweed.
