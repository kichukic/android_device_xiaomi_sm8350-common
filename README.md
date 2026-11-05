# Common Device Tree for Xiaomi SM8350 Devices

Common device configuration repository for Snapdragon 888 (SM8350, Lahaina) Xiaomi devices on **RisingOS 9 (Android 17 / SDK 37)**.

## Supported Devices

- Xiaomi Mi 11X Pro / Redmi K40 Pro / Mi 11i (`haydn`)
- Xiaomi Mi 11 (`venus`)
- Xiaomi Mi 11 Pro / Ultra (`star`)
- Xiaomi MIX 4 (`odin`)

## Common Configurations & Optimizations

- **Memory Management:**
  - Upgraded ZRAM compression to **Zstandard (`zstd`)** for high-efficiency ~3.2x compression ratio.
  - Disabled page deduplication (`use_dedup = 0`) to prevent background SHA256 CPU drain.
  - 8GB / 12GB Dalvik VM heap configuration (`phone-xhdpi-8192-dalvik-heap.mk`, 384MB heap growth limit).
- **Networking:**
  - Default TCP Congestion Control set to **Google BBR** (`net.ipv4.tcp_congestion_control=bbr`) in `init.qcom.rc` and `system.prop`.
- **Audio Stack:**
  - Integrated **Motorola Dolby Atmos (`MotoDolbyDax3`)** with `DSPVolumeSynchronizer`.
- **Stability Hardening:**
  - Early-boot enforcement of `panic=0` and `panic_on_oops=0` in `init.qcom.rc` to suppress random reboots from minor driver hiccups.
