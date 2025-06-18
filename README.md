# Intrusion_Detection_System
Intrusion is when an attacker gets unauthorized access to a device, network, or system. Cyber criminals use advanced techniques to sneak into organizations without being detected.  Intrusion Detection System (IDS) observes network traffic for malicious transactions and sends immediate alerts when it is observed. It is software that checks a network or system for malicious activities or policy violations.

SNORT is a powerful open-source intrusion detection system (IDS) and intrusion prevention system (IPS) that provides real-time network traffic analysis and data packet logging. SNORT uses a rule-based language that combines anomaly, protocol, and signature inspection methods to detect potentially malicious activity.


# 🛡️ Network-based Intrusion Detection System (NIDS) using Snort 3

This project showcases the setup of a **Network-based Intrusion Detection System (NIDS)** using **Snort 3** on Ubuntu. The goal is to monitor and analyze network traffic to detect potential threats using rule-based logic.

![image](https://github.com/user-attachments/assets/35dda460-7a4d-4f6f-85e8-ebfe6229ddca)

---

## 📚 What is Snort?

[Snort](https://www.snort.org/) is a powerful, open-source NIDS developed by Cisco. It uses a set of rules to detect malicious activity like port scans, buffer overflows, and more by inspecting network packets in real time.

---

## 🎯 Project Objectives

- ✅ Build a working NIDS using Snort 3
- ✅ Detect potential network threats using custom rules (local.rules)
- ✅ Understand and demonstrate packet inspection using the pcap DAQ
- ✅ Analyze alerts generated in real time
- ✅ Focus only on **local rule-based detection** (no pulledpork or community rules)

---

## 🖥️ Environment

- Ubuntu 20.04/22.04 (tested on VirtualBox)
- Snort version: 3.8.1.0
- Interface: `ens33` (update based on your setup)

---

## ⚙️ Installation Steps

### 1. System Update and Dependencies

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y build-essential autotools-dev libdumbnet-dev libluajit-5.1-dev \
libpcap-dev zlib1g-dev pkg-config libhwloc-dev cmake liblzma-dev openssl \
libssl-dev cpputest libsqlite3-dev libtool uuid-dev git autoconf bison flex \
libcmocka-dev libnetfilter-queue-dev libunwind-dev libpcre2-dev

**2. Install Hyperscan**
