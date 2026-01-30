##Packet-inspection-kali-homelab
<img width="1919" height="1079" alt="Screenshot 2026-01-16 110756" src="https://github.com/user-attachments/assets/a73ba6dd-93d6-4191-aaf8-233395558a82" />

# 🛡️ Project: Network Security Lab & Protocol Analysis
**Author:** Bekeh Aniekan
**Lab Environment: VirtualBox + Kali Linux + MTN MiFi

## 📺 Project Walkthrough
## 🏗️ Lab Architecture
* Host: Windows 10/11
* Guest VM: Kali Linux (Security Distribution)
* Connectivity: Bridged Wireless via MTN MiFi (Simulating a real-world mobile gateway)
* Primary Tool: Wireshark Protocol Analyzer

## 🕵️ Analysis & Incident Response
I conducted a deep-packet inspection (DPI) to monitor how data travels across the ISP gateway.

### 1. Discovery Path Mapping
Using `traceroute google.com`, I mapped the 12+ hops between my local lab and the destination server. I verified the **TTL (Time to Live)** value of 64, which fingerprints the source as a Linux-based system.
<img width="1919" height="1079" alt="Screenshot 2026-01-17 140014" src="https://github.com/user-attachments/assets/ded19398-a283-49c1-9441-9d49a07241c9" />

### 2. Incident Discovery: Plain-Text Vulnerability
During monitoring, I identified a high-severity risk where a login was performed over an unencrypted HTTP connection. 
* **Filter Used:** `http.request.method == "POST"`
* **Impact:** Captured raw credentials (Username/Password) in the packet bytes.
  <img width="1906" height="1036" alt="Screenshot 2026-01-30 113748" src="https://github.com/user-attachments/assets/03c6ddc7-5484-4c68-9aa6-8b63b05538c6" />
<img width="1910" height="502" alt="Screenshot 2026-01-30 113954" src="https://github.com/user-attachments/assets/81a6f03c-ca4a-455d-9fc9-e84a14bcebe7" />
<img width="1283" height="387" alt="Screenshot 2026-01-30 115418" src="https://github.com/user-attachments/assets/21a64f48-f1b6-4426-8058-da7298071f16" />



> [!IMPORTANT]
> **View the Full Incident Response Report here:** [Incident_Report_001.md](./Incident_Report_001.md)

## 🛠️ Challenges Overcome
* **Resolved VirtualBox Path Error:** Fixed `VERR_FILE_NOT_FOUND` by manually re-mapping the .vdi disk path after a directory mismatch.
* **Network Bridging:** Configured virtual network adapters to properly handshake with the MTN MiFi gateway for live sniffing.
