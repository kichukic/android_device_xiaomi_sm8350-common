# Common Tree Changelog for Xiaomi SM8350

## 2026-11-05 Release (RisingOS 9)

- **ZSTD ZRAM Backend:** Switched ZRAM compression engine to `zstd` across all SM8350 post-boot scripts (`post_boot-lahaina.sh`, `post_boot-shima.sh`, `post_boot-yupik.sh`).
- **Google BBR TCP:** Configured runtime default TCP congestion algorithm to BBR via `init.qcom.rc` and `system.prop`.
- **Motorola Dolby Audio:** Cleaned up and finalized Motorola Dolby Atmos audio effects integration with `DSPVolumeSynchronizer`.
- **Dalvik Heap Tuning:** Scaled Dalvik heap growth limit to 384MB to maximize multitasking retention on 8GB/12GB devices.
- **Kernel Panic Hardening:** Enforced `sys.oops.panic=0` and `kernel.panic=0` in early boot scripts.

### Storage, ART & Audio Tuning
- **UFS 3.1 I/O Optimization:**
  - Automated detection and tuning of UFS block devices (`/sys/block/sd*`).
  - Switched I/O scheduler to `kyber` (latency-optimized multi-queue scheduler) with `bfq` fallback.
  - Set optimal 128KB read-ahead buffer for random 4K flash throughput.
  - Disabled storage entropy pool contribution (`add_random=0`) and accounting stats (`iostats=0`) to eliminate CPU spinlocks.
  - Set queue depth to 64 requests.
- **ART & Dexopt Performance:**
  - Configured profile-guided AOT compilation (`speed-profile`) on app install and idle background dexopt.
  - Scaled parallel dex2oat threads to 6 (and 8 for boot) to leverage big/prime Kryo 680 cores.
- **UI Pacing & Smoothness:**
  - Tuned SurfaceFlinger 120Hz frame pacing offsets and touch timers (`set_touch_timer_ms=200`, `latch_unsignaled=1`).
  - Increased Home Launcher RAM pinning to 25MB (`config_pinnerHomePinBytes=26214400`) to completely eliminate launcher redraws after gaming.
- **Audio & Haptics:**
  - Enabled 24-bit / 192kHz Hi-Fi audio output (`vendor.audio.feature.hifi_audio.enable=true`, `vendor.audio.offload.24bit.enable=true`).
  - Doubled audio offload buffer size to 64KB to cut CPU wakeups and save battery during music playback.
  - Enabled 3-level granular vibration intensity slider (Low, Medium, High) in Settings.

### Bluetooth Audio & Framework Animation Physics
- **Bluetooth Audio Bitrate Uncap:**
  - Removed AAC bitrate whitelist caps (`persist.vendor.bt.a2dp.aac_whitelist=false`).
  - Enabled AAC VBR frame control.
  - Set default LDAC streaming profile to 990 kbps high-quality audio (`persist.bluetooth.ldac.rate=990`).
  - Decoupled Bluetooth absolute volume (`persist.bluetooth.disableabsvol=true`) to eliminate digital clipping on external DACs.
  - Disabled Bluetooth snoop debugging log to save CPU cycles.
- **Framework Animation Durations:**
  - Calibrated animation timings for 120Hz refresh rates: `shortAnimTime` (150ms), `mediumAnimTime` (250ms), `longAnimTime` (350ms), `activityShortDur` (120ms), `activityDefaultDur` (180ms).
