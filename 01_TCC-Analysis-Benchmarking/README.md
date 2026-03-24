# Project 01: System Profiling & Security Baseline Research
> **Technical Foundation:** Analysis of macOS Tahoe 26.3.1 TCC Mechanisms and M4 Pro GPU Performance Metrics.

---

## 1. Research Overview
This phase serves as the technical feasibility validation for the **Hetero-AutoWPAx** framework. By conducting empirical measurements of security constraints (TCC) and computational resource limits (GPU) within the latest Apple Silicon environment, we established the design rationale for Projects 02 and 03.

## 2. macOS Tahoe 26.3.1 TCC Analysis
Identified a bypass vector leveraging **'Privilege Asymmetry'** in environments where standard reconnaissance paths are obstructed by reinforced TCC policies.

* **Problem:** SSID masking (`<redacted>`) enforced on standard system utilities such as `system_profiler`.
* **Vulnerability:** Exceptional data access permitted via **Internal Entitlements** of the system bundle (`Wireless Diagnostics`).
    * `com.apple.locationd.preauthorized`
    * `com.apple.wifi.events.private`
* **Conclusion:** Validated the potential for **Privilege Hijacking** by exploiting the trust gap between system services and user-space processes.

## 3. Hardware Acceleration Performance
Empirical benchmarks for WPA2-CCMP handshake cracking utilizing the Apple M4 Pro (20-Core GPU) architecture.

### Performance Metrics
* **Throughput:** `241.4 kH/s` (PBKDF2-HMAC-SHA1 pipeline).
* **Compute Density:** Approximately **1.98 billion** SHA-1 compression function calls per second.
* **Power Efficiency:** `8.05 kH/s/W` (Approx. **39.2% superior** to NVIDIA RTX 4090).
* **UMA Impact:** Unified Memory Architecture (UMA) eliminated data transfer bottlenecks during large-scale dictionary processing via Zero-copy streaming.

## 4. Technical Specifications
| Category | Details |
| :--- | :--- |
| **OS Environment** | macOS Tahoe 26.3.1 (Build 26Dxx) |
| **Hardware** | Apple M4 Pro (14C CPU / 20C GPU) |
| **Tools Used** | `hcxpcapngtool`, `Hashcat v6.2.6`, `Wireless Diagnostics` |
| **Cracking Speed** | 241,400 hashes per second |
| **Success Case** | 14.45M Dictionary exhaustion in **~15 seconds** |

---

## 5. Artifacts
* **Research Paper:** [`Exploiting_TCC_and_Metal_Optimization_for_WPAx.pdf`](./paper/Exploiting_TCC_and_Metal_Optimization_for_WPAx.pdf)
* **Raw Benchmarks:** [`GPU_Throughput_M4Pro.csv`](./data/GPU_Throughput_M4Pro.csv)
* **Analysis Logs:** [`TCC_Privilege_Mapping.log`](./logs/TCC_Privilege_Mapping.log)

---
*This research serves as the technical baseline for Project 02 (Native Metal API Implementation).*
