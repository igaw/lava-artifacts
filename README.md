# lava-artifacts

Kernel images, device trees and NFS rootfs archives for the LAVA health
checks of a private test lab. They cover the PREEMPT_RT builds that
[montjoie/lava-healthchecks-binary](https://github.com/montjoie/lava-healthchecks-binary)
doesn't have: it tracks mainline and stable kernels.

The files are assets of this repo's
[releases](https://github.com/igaw/lava-artifacts/releases), not git
objects, so a clone stays small and downloads need no Git LFS quota. A
release is one kernel version and is never changed; a new version is a
new release, and the tag and the suffix of each kernel's name say which
one it is.

```
https://github.com/igaw/lava-artifacts/releases/download/<tag>/<file>
```

## v4.19.325-rt140

Five kernel variants per board, with different scheduling and latency
configs: `up`, `ll`, `vp`, `nohz`, `rt`.

| Board | LAVA device type | Kernels | Device tree | Rootfs |
|---|---|---|---|---|
| c2d | `x86` (boots via iPXE) | `c2d-image-<variant>-v4.19.325-rt140` | none | `lava-image.x86_64-1.tar.xz` |
| bbb | `beaglebone-black` | `bbb-image-<variant>-v4.19.325-rt140` | `am335x-boneblack.dtb` | `lava-image.armv7l-1.tar.xz` |
| rpi3-64 | `bcm2837-rpi-3-b` | `rpi3-64-image-<variant>-v4.19.325-rt140` | `bcm2837-rpi-3-b-plus.dtb` | `lava-image.aarch64-1.tar.xz` |

The health checks use the `rt` variant of each board. The other
variants aren't referenced by a job.

The rootfs archives are for test boards only: root has an empty
password.

## Sources

- Kernels: tag `v4.19.325-rt140` of
  [linux-stable-rt](https://git.kernel.org/pub/scm/linux/kernel/git/rt/linux-stable-rt.git).
  Configs and local patches: TODO.
- Rootfs: built with KIWI NG from
  [igaw/kiwi-lava](https://github.com/igaw/kiwi-lava), openSUSE Tumbleweed
  from August 2022.
