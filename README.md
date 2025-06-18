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
```

---

### 2. Install Hyperscan

```bash
git clone https://github.com/intel/hyperscan.git
cd hyperscan
mkdir build && cd build
cmake ..
make -j$(nproc)
sudo make install
```

---

### 3. Install Flatbuffers

```bash
git clone https://github.com/google/flatbuffers.git
cd flatbuffers
mkdir build && cd build
cmake ..
make -j$(nproc)
sudo make install
```

---

### 4. Install DAQ

```bash
cd ~
wget https://www.snort.org/downloads/snort/daq-3.0.13.tar.gz
tar -xvzf daq-3.0.13.tar.gz
cd daq-3.0.13
./configure
make -j$(nproc)
sudo make install
```

---

### 5. Install Snort 3

```bash
cd ~
wget https://github.com/snort3/snort3/archive/refs/tags/3.8.1.0.tar.gz -O snort3-3.8.1.0.tar.gz
tar -xvzf snort3-3.8.1.0.tar.gz
cd snort3-3.8.1.0
./configure_cmake.sh --prefix=/usr/local --enable-tcmalloc
cd build
make -j$(nproc)
sudo make install
```

---

## 🔧 Configuration

### 1. Create Required Directories

```bash
sudo mkdir -p /usr/local/etc/snort/rules
sudo mkdir /usr/local/etc/snort/so_rules
sudo mkdir /usr/local/etc/snort/lists
sudo mkdir /var/log/snort
```

---

### 2. Copy Default Config Files

```bash
cd ~/snort3-3.8.1.0/etc
sudo cp *.lua /usr/local/etc/snort/
sudo cp snort_defaults.conf /usr/local/etc/snort/
```

---

### 3. Create Local Rules

```bash
sudo nano /usr/local/etc/rules/local.rules
```

Add this rule to detect ICMP:

```snort
alert icmp any any -> any any (msg:"ICMP Packet Detected"; sid:1000001; rev:1;)
```

---

### 4. Update `snort.lua` to Use Local Rules

Edit:

```bash
sudo nano /usr/local/etc/snort/snort.lua
```

Modify the `ips` section like this:

```lua
ips =
{
  enable_builtin_rules = true,
  include = '/usr/local/etc/rules/local.rules',
}
```

---

## 🚀 Running Snort

Use the following command to run Snort with your local rules:

```bash
sudo snort -c /usr/local/etc/snort/snort.lua -R /usr/local/etc/rules/local.rules -i ens33 -A alert_fast
```

> Replace `ens33` with your actual interface (`ip a` to check).

---

## 🛠️ Troubleshooting

- `Couldn't start DAQ instance`: Run with `sudo` and correct interface.
- `FATAL: see prior 290 errors`: Likely config or rule syntax error.
- `ld terminated with signal 9`: Means RAM was full, increase system memory.
- If `libpcap` is missing, check if installed: `sudo apt install libpcap-dev`.

---

## ✅ Summary

- You installed Snort 3 with all necessary dependencies.
- Configured and tested a basic local rule-based IDS.
- Can detect and alert on simple network activity like pings.

---

