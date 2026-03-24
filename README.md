# Hetero-AutoWPAx
**A Heterogeneous Collaborative Full-Chain Automated Penetration Framework for WPAx**

## Abstract
Hetero-AutoWPAx is a research-driven framework designed to bridge the gap between high-performance macOS hardware and distributed edge computing for automated WPA/WPA2/WPA3 security auditing. The project shifts from manual tool-chaining to a programmatic "Full-Chain" approach, leveraging the Apple Silicon architecture (GPU/Neural Engine) alongside Linux-based ARM nodes (Raspberry Pi) to achieve a collaborative, automated exploitation pipeline.

---

## Project Roadmap: From Testing to Framework Orchestration

### Project 01: TCC Analysis & Performance Benchmarking
The initial phase focuses on reconnaissance and baseline performance testing within the restricted environment of **macOS Tahoe 26.3.1**. 
* **TCC Security Analysis:** Analyzing the Transparency, Consent, and Control (TCC) framework to identify non-standard permission acquisition for raw network interface monitoring.
* **GPU Performance Profiling:** Benchmarking the 20-core GPU on Apple Silicon to evaluate its computational throughput for parallelized cryptographic operations compared to traditional x86-64 environments.

### Project 02: Native Scanning Engine & Metal-Kernel Optimization
The second phase transitions from testing to active system implementation, focusing on deep OS integration.
* **Privileged Process Entitlement Research:** Investigating the hijacking of specific entitlements within Apple System Bundles to facilitate automated, silent reconnaissance on macOS.
* **Autonomous Scanning & Sniffing Engine:** Developing a native engine for low-level packet interaction. In the event of macOS privilege restrictions, the development pivots to a dedicated Linux-based engine for stable packet injection and handshake monitoring.
* **Metal API Kernel Orchestration:** Engineering a GPU-accelerated processing unit via the **Metal API**. This involves direct kernel-level orchestration to leverage Apple Silicon’s **Unified Memory Architecture (UMA)**. By implementing **zero-copy data transfer** between the CPU and GPU, the framework minimizes memory overhead, significantly optimizing throughput for real-time packet filtering and parallelized hash pre-computation.
  
### Project 03: Distributed Collaborative Framework Construction
The final phase integrates the developed modules into a cohesive, heterogeneous "Full-Chain" system.
* **Collaborative Architecture:** Deploying Raspberry Pi nodes as distributed sensors for automated handshake collection (Capture Nodes) while offloading heavy-duty processing to the macOS-based command center (Analysis/Cracking Node).
* **Auto Full-Chain Pipeline:** A seamless link between:
    1.  **Automated Collection:** Distributed sniffing and capture of EAPOL frames.
    2.  **Stateful Analysis:** Real-time validation of captured handshakes.
    3.  **Distributed Cracking:** Orchestrated hash analysis leveraging the previously developed Metal-based GPU engine.
* **System Finalization:** Completing the autonomous pipeline where a single trigger initiates the entire sequence from proximity detection to successful credential recovery.

### Collaborative Framework Architecture

```mermaid
graph TD
    subgraph "Central Orchestrator (macOS - Apple Silicon)"
        M[MacBook Pro] -- Metal API --> G[20-Core GPU]
        G -- Parallelized Cracking --> C[Credential Recovery]
        M -- C2 Orchestration --> O[Task Dispatcher]
    end

    subgraph "Distributed Edge Nodes (Linux - ARM)"
        R1[Raspberry Pi Node 1] -- Sniffing --> P1[EAPOL Frames]
        R2[Raspberry Pi Node 2] -- Sniffing --> P2[EAPOL Frames]
        RN[Raspberry Pi Node N] -- Sniffing --> PN[EAPOL Frames]
    end

    P1 -- Handshake Upload --> M
    P2 -- Handshake Upload --> M
    PN -- Handshake Upload --> M
    O -- Command --> R1
    O -- Command --> R2
    O -- Command --> RN

    style M fill:#f9f,stroke:#333,stroke-width:2px;
    style G fill:#ccf,stroke:#333,stroke-width:2px;
    style R1 fill:#ff9,stroke:#333;
    style R2 fill:#ff9,stroke:#333;
    style RN fill:#ff9,stroke:#333;

---

## Technical Specifications
* **Primary Environment:** macOS Tahoe 26.3.1 (Apple Silicon 20-Core GPU)
* **Secondary Environment:** Linux (Debian/Kali-based ARM for Raspberry Pi)
* **Core Technologies:** Metal API, C++/Swift for Kernel interaction, Distributed Network Orchestration.

---

## Legal Disclaimer
This framework is intended for professional security research and authorized penetration testing only. The author holds no responsibility for unauthorized use or damages resulting from the application of this research. Use of these tools in environments without explicit consent is strictly prohibited by law.

## License
Licensed under the GNU General Public License v3.0 (GPLv3).
