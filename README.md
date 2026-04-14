# MikuChan Kernel — Realme 6 (MT6785/G90T)

![MikuChan Banner](https://img.shields.io/badge/Kernel-MikuChan-blue?style=for-the-badge&logo=linux)
![Platform](https://img.shields.io/badge/Platform-MediaTek%20MT6785-orange?style=for-the-badge)
![Android](https://img.shields.io/badge/Android-15+-green?style=for-the-badge&logo=android)

MikuChan Kernel is a high-performance, feature-rich custom kernel specifically optimized for the **Realme 6 series** and other **MediaTek MT6785 (Helio G90T)** devices. This kernel is designed to bridge the gap between stock stability and bleeding-edge performance, with full support for Android 15+ custom ROMs.

---

## 📱 Supported Devices

The kernel supports all Realme devices based on the **RM6785** platform:

- **Realme 6** (RMX2001)
- **Realme 6i / 6S** (RMX2002)
- **Realme 7** (RMX2151)
- **Realme Narzo 20 Pro** (RMX2161)
- **Realme Narzo 30 4G** (RMX2156)

---

## 🔥 Key Implementations & Features

### 🚀 Performance Overclocking (OC)

- **CPU Overclock**: The big cluster (Cortex-A76) has been pushed from **2.05GHz to 2.20GHz**. Balanced with a conservative +31.25mV voltage bump (1.150V) for sustained stability.
- **GPU Overclock**: The Mali-G76 MC4 frequency ceiling has been unlocked from **821MHz to 900MHz**. This is achieved by removing artificial segment caps in the `mtk_gpufreq` driver.

### 📶 Connectivity & Handshake Fixes

- **5GHz Hotspot/AP**: Fixed the "disabled" status on 5GHz channels. Explicitly enables UNII-1 (36-48) and UNII-3 (149-165) bands and resolves regulatory domain mismatches for the Indian (IN) market.
- **WPA3-SAE Support**: Fully enabled support for Simultaneous Authentication of Equals (SAE). Includes `Curve25519` and `ChaCha20-Poly1305` crypto primitives in the kernel for secure, modern handshakes.

### 🤖 Android 15+ & Future-Proofing

- **EBPF Support**: Fully enabled `CONFIG_BPF_SYSCALL`, `BPF_JIT`, and `CGROUP_BPF` required for modern Android security and monitoring tools.
- **BinderFS**: Implemented Android Binder Filesystem support for better containerization and compatibility with the latest Android HALs.
- **LRU Gen**: (MGLRU) support for better memory management under heavy multitasking.

### 🎮 Gaming & MediaTek HyperEngine 1.0

- **Full GED/FPSGO Support**: All Gaming Enhancement Device (GED) nodes are active, including `gx_game_mode` and `boost_gpu_enable`.
- **Smart Link Aggregation (SLA)**: Integrated `oplus_sla` for concurrent WiFi+LTE data usage to reduce latency spikes.
- **180Hz Touch Rate**: Full support for Novatek NT36672C touch panels with game mode reporting enabled.

### 🛠️ Kernel Tweaks & Optimization

- **TCP Congestion Control**: BBR (Google), Westwood, BIC, and Hybla enabled. Default set to `bbr` for superior throughput on varied networks.
- **I/O Schedulers**: Kyber and Deadline enabled. Optimized for UFS/EMMC storage nodes used in performance tuning scripts.
- **Memory Management**: Transparent Huge Pages (THP) with `madvise` support and ZRAM using `zstd` compression for the best balance of speed and compression ratio.

---

## 📦 Stock Realme Features Preserved

We maintain 100% compatibility with essential stock firmware components:

- ✅ **OPLUS Charger**: Full VOOC, DASH, and Quick Charge support.
- ✅ **OPPO HANS**: (Hyper Animation Networking Service) preserved for ROM stability.
- ✅ **Fingerprint Integration**: Correct nodes for FPC and Goodix fingerprint sensors.
- ✅ **Kernel Health**: Persistent OPLUS Healthinfo and performance nodes.

---

## 🛠️ Build Instructions

### Requirements

- **Toolchain**: Clang 20.0.0 or higher.
- **Cross Compiler**: AARCH64 and ARM Linux GNU cross-tools.
- **FS**: Case-sensitive filesystem is mandatory for building MediaTek connectivity drivers.

### Steps

1. Clone the source:
   ```bash
   git clone https://github.com/lowkeyarhan/RM6785-kernel.git
   ```
2. Set up the environment:
   ```bash
   export ARCH=arm64
   export SUBARCH=arm64
   ```
3. Initialize the config:
   ```bash
   make RM6785_defconfig
   ```
4. Build:
   ```bash
   make -j$(nproc)
   ```

---

## 📜 Credits

- **Realme / MediaTek**: For the base kernel source.
- **Zenitsu Kernel Team**: For Silicon OC references.
- **MikuChan Team**: For continuous optimization and maintenance.

---

> [!CAUTION]
> Overclocking frequencies and voltages can increase heat generation. Use a high-quality thermal pad or environment if running continuous stress tests.

---

_Developed with ❤️ for the Realme 6 Community._
