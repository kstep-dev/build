# build/

Per-kernel build artifacts for [kSTEP](https://github.com/kstep-dev/kstep). Submodule of the parent repo.

`<KERNEL>` is the build name set by `checkout.py` (defaults to the git ref, e.g. `v7.0`; `reproduce.py` uses `<bug>_buggy` / `<bug>_fixed`).

## Layout

```
build/
├── current → <KERNEL>/        symlink to the active build (set by checkout.py)
├── master/                    bare git clone reused by `checkout.py --git`
├── user                       statically-linked userspace binary (kernel-agnostic)
└── <KERNEL>/
    ├── kernel                 ✓ bootable image (bzImage / Image)
    ├── rootfs.cpio            ✓ initramfs (user + kmod.ko)
    ├── vmlinux                debug kernel for addr2line / gdb
    ├── linux/                 kernel source tree (tarball or worktree)
    ├── kmod/                  out-of-tree kmod build dir
    ├── rootfs/                staging dir for rootfs.cpio
    ├── build.log              `make linux` / `make kstep` log
    ├── compile_commands.json  clangd db (project root symlinks to `current/`)
    └── <ref>.tar.xz           kernel tarball (`--tar` only)
```

✓ tracked in git; everything else is regeneratable.
