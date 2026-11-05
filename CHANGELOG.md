# Common Tree Changelog for Xiaomi SM8350

## 2026-11-05 Release (RisingOS 9)

- **ZSTD ZRAM Backend:** Switched ZRAM compression engine to `zstd` across all SM8350 post-boot scripts (`post_boot-lahaina.sh`, `post_boot-shima.sh`, `post_boot-yupik.sh`).
- **Google BBR TCP:** Configured runtime default TCP congestion algorithm to BBR via `init.qcom.rc` and `system.prop`.
- **Motorola Dolby Audio:** Cleaned up and finalized Motorola Dolby Atmos audio effects integration with `DSPVolumeSynchronizer`.
- **Dalvik Heap Tuning:** Scaled Dalvik heap growth limit to 384MB to maximize multitasking retention on 8GB/12GB devices.
- **Kernel Panic Hardening:** Enforced `sys.oops.panic=0` and `kernel.panic=0` in early boot scripts.
