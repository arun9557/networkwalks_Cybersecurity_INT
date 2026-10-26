<div align="center">

# 🔐 Cybersecurity & Pentesting Lab Setup

**Building an isolated virtual lab environment using VirtualBox and Kali Linux for penetration testing and ethical hacking practice**

</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/VirtualBox-v7.x-0070C0?style=flat-square&labelColor=000000&logo=virtualbox&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2024%2B-557C94?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Batch-B084-E87500?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/NetworkWalks-Academy-C00000?style=flat-square" />
  <img src="https://img.shields.io/badge/GitHub-arun9557-0070C0?style=flat-square&logo=github&logoColor=white" />
</p>

---

## 📌 Project Overview

This project focuses on building an **isolated, dedicated virtual cybersecurity and penetration-testing laboratory** on a Windows host using Oracle VirtualBox and Kali Linux.

The primary goal is to establish a secure, controlled sandbox where offensive security tools, network reconnaissance, port scanning, vulnerability discovery, and packet analysis can be executed safely without exposing or damaging the host operating system or the local home/corporate network.

The lab network is configured using a custom **NAT Network** (`10.0.0.0/24`), enabling future target machines (such as Windows 10, Windows 11, Metasploitable, Windows Server, and Android) to be added to the exact same broadcast domain for authorized red-team and blue-team practice.

---

## 🎯 Objectives (TASK WK1-PM1)

The key objectives executed in this project module:

- [x] Install and configure Oracle VM VirtualBox and 7-Zip on the host computer.
- [x] Set up a custom **NAT Network** with subnet `10.0.0.0/24` and active DHCP service.
- [x] Download and import the pre-built Kali Linux Virtual Machine into VirtualBox.
- [x] Configure Virtual Machine enhancements:
  - **Shared Clipboard:** Bidirectional
  - **Drag and Drop:** Bidirectional
  - **Shared Folder:** `/downloads` mapped to host machine downloads directory.
- [x] Assign a consistent static IPv4 configuration to Kali Linux:
  - **IP Address:** `10.0.0.2/24`
  - **Default Gateway:** `10.0.0.1`
  - **DNS Server:** `8.8.8.8` (or `10.0.0.1`)
- [x] Verify complete outbound Internet access and DNS resolution from Kali Linux.
- [x] Resolve common network bugs (DAD timeout / NetworkManager bug on VirtualBox v7).
- [x] Capture a clean baseline **VM Snapshot** for instant recovery.
- [x] Document the architecture, configuration parameters, testing results, and troubleshooting steps.

---

## 🛡️ Purpose & Importance of the Lab

A virtualized cyber lab provides an ethical, isolated testing ground necessary for:

- **Network Reconnaissance & Host Discovery:** Scanning networks using `nmap`, `arp-scan`, `netdiscover`.
- **Vulnerability Assessment:** Testing for outdated services and configuration flaws.
- **Packet & Traffic Analysis:** Capturing and inspecting live network packets using `Wireshark` and `tcpdump`.
- **Payload & Exploit Research:** Safely evaluating security exploits without legal or collateral risks.
- **Defense Simulation:** Understanding how firewalls and IDS/IPS systems detect attack signatures.

> ⚠️ **Ethical Disclaimer:** This lab environment is strictly intended for educational and authorized penetration testing exercises. All activities are confined within an isolated private virtual network. Never perform scanning or testing on unauthorized external networks or systems.

---

## 🏗️ Lab Architecture & Network Topology

```
+---------------------------------------------------------------------------------------+
|                               HOST MACHINE (Windows 10 / 11)                          |
|                               Local Physical IP: 192.168.x.x / DHCP                   |
+---------------------------------------------------------------------------------------+
                                           │
                                           ▼ (VirtualBox Hypervisor Engine)
+---------------------------------------------------------------------------------------+
|                       VIRTUALBOX CUSTOM NAT NETWORK (Name: NatNetwork)                |
|                       Subnet: 10.0.0.0/24 | Default Gateway: 10.0.0.1                 |
|                       DHCP Pool Range: 10.0.0.2 - 10.0.0.99                           |
+---------------------------------------------------------------------------------------+
           │                                 │                              │
           ▼                                 ▼ (Future Target)              ▼ (Future Target)
+------------------------+      +------------------------+      +------------------------+
|   ATTACKER MACHINE     |      |    TARGET MACHINE 1    |      |    TARGET MACHINE 2    |
|   Kali Linux VM        |      |    Windows 10 / 11 VM  |      |    Android 9x VM       |
|   IP: 10.0.0.2/24      |      |    IP: 10.0.0.10/24    |      |    IP: 10.0.0.9/24     |
|   Gateway: 10.0.0.1    |      |    Gateway: 10.0.0.1   |      |    Gateway: 10.0.0.1   |
|   DNS: 8.8.8.8         |      |    Status: Optional    |      |    Status: Optional    |
+------------------------+      +------------------------+      +------------------------+
```

---

## ⚙️ Lab Configuration Specifications

| 🧩 Component | ⚙️ Specification / Setting | 📝 Notes |
| :--- | :--- | :--- |
| **🖥️ Host Operating System** | Windows 10 / 11 (64-bit) | Host physical machine |
| **🧠 Host RAM Allocation** | Minimum 8 GB (Allocated 2048 MB to VM) | 4096 MB recommended if host has 16GB RAM |
| **🧰 Hypervisor Software** | Oracle VM VirtualBox (v7.x) | Base virtualization layer |
| **🐉 Attacker OS** | Kali Linux (Pre-built VirtualBox Image) | Offensive security toolset |
| **🌐 Virtual Network Mode** | **NAT Network** (`NatNetwork`) | Allows multi-VM communication + outbound Internet |
| **📡 Network Subnet / Prefix**| `10.0.0.0/24` (Netmask: `255.255.255.0`) | Private Class A subnet |
| **🚪 Virtual Gateway** | `10.0.0.1` | VirtualBox NAT Gateway |
| **🐧 Kali Linux Static IP** | `10.0.0.2/24` | Attacker machine static address |
| **🌍 Primary DNS Server** | `8.8.8.8` (Fallback: `10.0.0.1`) | Google Public DNS |
| **📋 Clipboard & Drag-Drop** | **Bidirectional** | VM Settings -> General -> Advanced |
| **📂 Shared Folder** | Host `Downloads` ➔ `/downloads` | Auto-mount: Enabled, Access: Full |
| **🎯 Future Target IP Pool** | `10.0.0.3` to `10.0.0.99` | Reserved for victim VMs |

---

# 🪜 Step-by-Step Lab Setup Procedure

### Step 1: Install 7-Zip Archiver
1. Downloaded 64-bit 7-Zip from the official website: [https://7-zip.org/download.html](https://7-zip.org/download.html).
2. Installed 7-Zip to extract `.7z` compressed VirtualBox Kali VM archives.

<p align="center">
  <img src="./7%20ZIP%20WEBPAGE.jpg" alt="7-Zip Official Download Page" width="70%" />
  <br><em>Figure 1: 7-Zip Official Download Page</em>
</p>

<p align="center">
  <img src="./7%20ZIP%20SUCCESFULL%20INSTALLED%20SS.jpg" alt="7-Zip Installed Successfully" width="70%" />
  <br><em>Figure 2: 7-Zip Successfully Installed</em>
</p>

---

### Step 2: Install VirtualBox & Extension Pack
1. Downloaded Oracle VM VirtualBox for Windows: [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads).
2. Installed VirtualBox with default networking drivers and VirtualBox USB support.
3. Downloaded and installed the **VirtualBox Extension Pack** for USB 2.0/3.0 support and bidirectional clipboard integration.

<p align="center">
  <img src="./VIRTUAL%20BOX%20WEB%20PAGE.jpg" alt="VirtualBox Official Download Page" width="70%" />
  <br><em>Figure 3: VirtualBox Official Download Page</em>
</p>

<p align="center">
  <img src="./VIRTUAL%20BOX%20INSTALED%20SS.jpg" alt="VirtualBox Installed Successfully" width="70%" />
  <br><em>Figure 4: VirtualBox Installed Successfully</em>
</p>

---

### Step 3: Create the Custom NAT Network in VirtualBox
A dedicated **NAT Network** was created instead of default NAT so all present and future virtual machines can discover and attack each other on the same subnet while maintaining outbound internet.

**Configuration steps:**
1. Navigated to VirtualBox Manager: **File** ➔ **Tools** ➔ **Network**.
2. Switched to the **NAT Networks** tab and clicked **Create (+)**.
3. Configured properties:
   - **Name:** `NatNetwork`
   - **IPv4 Prefix:** `10.0.0.0/24`
   - **Enable DHCP:** `Checked` ✅
   - **Enable IPv6:** `Unchecked` ❌
4. Clicked **Apply**.

<p align="center">
  <img src="./VirtualBox%20me%20Custom%20NATNetwork%20Banayein%20-%20COMPLETED%20SS.jpg" alt="VirtualBox Custom NATNetwork Configuration" width="75%" />
  <br><em>Figure 5: Custom NATNetwork (10.0.0.0/24) Created in VirtualBox</em>
</p>

---

### Step 4: Import and Configure Kali Linux VM
1. Downloaded the official pre-built VirtualBox image (`.7z`) from [kali.org/get-kali](https://www.kali.org/get-kali/#kali-virtual-machines).
2. Extracted the archive using 7-Zip.
3. In VirtualBox, selected **Machine** ➔ **Add** and imported the extracted `.vbox` file.

<p align="center">
  <img src="./KALI%20LINUX%20WEB%20PAGE.jpg" alt="Kali Linux Pre-built VM Download Page" width="70%" />
  <br><em>Figure 6: Kali Linux Pre-built VM Download Page</em>
</p>

<p align="center">
  <img src="./KALI%20LINUX%20DOWLOADING%20IN%20PROCESS.jpg" alt="Kali Linux Downloading in Process" width="70%" />
  <br><em>Figure 7: Kali Linux Image Download in Progress</em>
</p>

4. Opened **VM Settings** and configured the following parameters:
   - **General ➔ Advanced:**
     - Shared Clipboard: `Bidirectional`
     - Drag'n'Drop: `Bidirectional`
   - **System ➔ Motherboard & Processor:**
     - Base Memory: `2048 MB` (or `4096 MB`)
     - Processors: `2 CPUs`
   - **Network ➔ Adapter 1:**
     - Attached to: `NAT Network`
     - Name: `NatNetwork`
     - Adapter Type: `Intel PRO/1000 MT Desktop (82540EM)`
     - Promiscuous Mode: `Allow All`
     - Cable Connected: `Checked` ✅
   - **Shared Folders:**
     - Path: Host machine `Downloads` folder
     - Name: `downloads`
     - Auto-mount: `Checked` ✅

<p align="center">
  <img src="./kali%20linux%20details%20.jpg" alt="Kali Linux VM Configuration Details" width="75%" />
  <br><em>Figure 8: Kali Linux System and Hardware Configuration</em>
</p>

<p align="center">
  <img src="./Network%20%20Adapter%201.jpg" alt="Kali Linux Network Adapter Settings" width="75%" />
  <br><em>Figure 9: Network Adapter 1 set to NatNetwork with Promiscuous Mode Allow All</em>
</p>

---

### Step 5: Configure Static IP Address on Kali Linux
1. Started the Kali VM and logged in with default credentials (`kali` / `kali`).
2. Right-clicked the network tray icon in the upper-right corner and selected **Edit Connections...**.
3. Selected **Wired connection 1** and clicked the **Settings (gear)** icon.
4. Navigated to the **IPv4 Settings** tab:
   - **Method:** `Manual`
   - Clicked **Add** under Addresses:
     - **Address:** `10.0.0.2`
     - **Netmask:** `24`
     - **Gateway:** `10.0.0.1`
   - **DNS Servers:** `8.8.8.8` (or `10.0.0.1`)
5. Clicked **Save**.

<p align="center">
  <img src="./Static%20IP%20set%20karne%20ke%20liye%20ss.jpg" alt="Static IP Configuration on Kali Linux" width="75%" />
  <br><em>Figure 10: Setting Static IP 10.0.0.2, Netmask 24, Gateway 10.0.0.1 and DNS 8.8.8.8</em>
</p>

---

### Step 6: Fix Internet Connectivity (VirtualBox v7 DAD Timeout Workaround)
On recent VirtualBox v7 releases with Kali Linux, Duplicate Address Detection (DAD) can prevent the static connection from activating properly.

The issue was resolved via terminal:
```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

---

### Step 7: Capture Baseline Clean Snapshot
1. Gracefully shut down the Kali Linux VM.
2. Selected the Kali VM in VirtualBox Manager and navigated to **Snapshots**.
3. Clicked **Take Snapshot**:
   - **Snapshot Name:** `Fresh Install - Working Network`
   - **Description:** `Kali Linux 10.0.0.2 static IP with NatNetwork and working internet connectivity.`

---

# 🔎 Lab Verification & Connectivity Tests

The lab configuration was verified using the following diagnostic tests:

| 🧪 Verification Test | 💻 Terminal Command | 🎯 Expected Output | 📊 Result |
| :--- | :--- | :--- | :---: |
| **Verify Static IP** | `ip a` | `inet 10.0.0.2/24 brd 10.0.0.255 scope global eth0` | PASS ✅ |
| **Verify Gateway Reachability** | `ping -c 4 10.0.0.1` | `4 packets transmitted, 4 received, 0% packet loss` | PASS ✅ |
| **Verify Public Internet Access** | `ping -c 4 8.8.8.8` | `4 packets transmitted, 4 received, 0% packet loss` | PASS ✅ |
| **Verify DNS Name Resolution** | `nslookup networkwalks.com` | Resolves authoritative IP address for domain | PASS ✅ |
| **Verify Nmap Security Tool** | `nmap --version` | Outputs installed Nmap version | PASS ✅ |
| **Verify Snapshot Restore** | Restore Snapshot & re-check `ip a` | Machine reverts to clean working state | PASS ✅ |

### Terminal Verification Output Snippet:
```text
┌──(kali㉿kali)-[~]
└─$ sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"

Connection 'Wired connection 1' successfully deactivated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/5)
Connection successfully activated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/6)
                                                                             
┌──(kali㉿kali)-[~]
└─$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:c3:fb:76 brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.2/24 brd 10.0.0.255 scope global noprefixroute eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::7882:4125:28ce:8cb3/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever

┌──(kali㉿kali)-[~]
└─$ ping -c 4 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=111 time=90.2 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=111 time=58.6 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=111 time=35.0 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=111 time=32.7 ms

--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3048ms
rtt min/avg/max/mdev = 32.742/54.165/90.228/23.157 ms

┌──(kali㉿kali)-[~]
└─$ ping -c 4 google.com
PING google.com (172.217.26.14) 56(84) bytes of data.
64 bytes from tzdelb-ay-in-f14.1e100.net (172.217.26.14): icmp_seq=1 ttl=112 time=33.2 ms
64 bytes from tzdelb-ay-in-f14.1e100.net (172.217.26.14): icmp_seq=2 ttl=112 time=158 ms
64 bytes from tzdelb-ay-in-f14.1e100.net (172.217.26.14): icmp_seq=3 ttl=112 time=36.7 ms
64 bytes from tzdelb-ay-in-f14.1e100.net (172.217.26.14): icmp_seq=4 ttl=112 time=52.2 ms

--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3640ms
rtt min/avg/max/mdev = 33.212/70.125/158.460/51.497 ms
```


---

# 🐞 Problems Encountered & Troubleshooting

### Problem 1: No Internet Access After Setting Static IP
- **Symptom:** Network connection showed "Connecting..." or disconnected after setting static IP `10.0.0.2`.
- **Root Cause:** VirtualBox v7 ARP response timing conflicts with Linux Duplicate Address Detection (`dad-timeout`).
- **Solution:** Disabled IPv4 DAD timeout using `nmcli`:
  ```bash
  sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
  sudo nmcli connection up "Wired connection 1"
  ```

### Problem 2: VirtualBox VT-x / AMD-V Hardware Virtualization Disabled
- **Symptom:** Virtual machine fails to power on with error `VT-x is disabled in the BIOS for all CPU modes`.
- **Solution:** Rebooted the host machine, entered UEFI/BIOS firmware settings, enabled **Intel Virtualization Technology (VT-x)** / **AMD SVM**, and saved changes.

### Problem 3: Standard NAT vs NAT Network Misconfiguration
- **Symptom:** Selecting default "NAT" isolates the VM behind its own individual router, preventing communication with other target VMs.
- **Solution:** Switched the adapter attachment to **NAT Network** with name `NatNetwork` to create a shared virtual switch for all VMs.

---

# 💡 Key Learnings & Takeaways

1. **NAT vs NAT Network Architecture:** Standard NAT isolates each VM into its own unique sandbox. A **NAT Network** acts like a physical virtual switch connected to a router, allowing all connected VMs to discover each other while sharing internet access.
2. **Promiscuous Mode (`Allow All`):** Required for packet capturing, network sniffing, and Man-in-the-Middle (MITM) simulations where network adapters need to inspect packets not destined for their own MAC address.
3. **Snapshot Management:** Establishing a pristine baseline snapshot before downloading payloads or launching exploits ensures instantaneous recovery without having to reinstall the operating system.
4. **Professional Technical Documentation:** Clean markdown documentation with architecture schematics, tables, and verifiable evidence is an essential industry skill for penetration testing and client reporting.

---

# 🔗 Tools & References

- **7-Zip Archiver:** [https://7-zip.org/download.html](https://7-zip.org/download.html)
- **Oracle VM VirtualBox:** [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
- **Kali Linux Official Downloads:** [https://www.kali.org/get-kali](https://www.kali.org/get-kali)
- **NetworkWalks Academy:** [https://www.networkwalks.com](https://www.networkwalks.com)

---

# 👤 Author Information

- **Name:** Arun
- **Program:** Cybersecurity Internship (Batch B084) — NetworkWalks Academy
- **Module:** Week 1 — Project Module 1 (TASK WK1-PM1)
- **GitHub Repository:** [arun9557/networkwalks_Cybersecurity_INT](https://github.com/arun9557/networkwalks_Cybersecurity_INT)
