[lab_guide (1).md](https://github.com/user-attachments/files/34510274/lab_guide.1.md)
# Network Traffic Analysis & Incident Response Lab (Activity 10)

An educational hands-on cybersecurity laboratory activity focusing on network packet analysis, forensic artifact extraction, and incident ticket documentation using **Wireshark**, **NetworkMiner**, and an interactive **Incident Ticket Worksheet**.

---

## 📌 Activity Overview

In **Activity 10**, students assume the role of a Tier-1 Incident Response Analyst inspecting a pre-captured network packet file (`networkinvestigation2.pcap`). Students will perform deep packet inspection in **Kali Linux** using **Wireshark** to analyze raw protocol streams and **NetworkMiner** to extract host metadata, credentials, transmitted files, and URI parameters. 

All forensic findings, cryptographic hashes, and mitigation strategies must be documented inside the provided `CyberAttack_Incident_Ticket_Interactive_Final.xlsx` template.

---

## 🎯 Learning Objectives

By completing this laboratory activity, students will be able to:

1. **Perform Forensic Packet Inspection:** Analyze cleartext HTTP headers, query strings, User-Agents, and network streams using Wireshark display filters.
2. **Automate Artifact Extraction:** Utilize NetworkMiner to parse host profiles, session files, cleartext credentials, and URI parameters from `.pcap` files.
3. **Verify Integrity & Cryptographic Hashes:** Calculate file hashes (`SHA-256`) for target capture files and extracted payloads.
4. **Incident Response Reporting:** Classify threats using standardized NIST frameworks, determine attack severity, and complete interactive incident tickets with drop-down validation menus.

---

## 🧰 Prerequisites & System Requirements

* **Environment:** Kali Linux 64-bit Virtual Machine (or dual-boot host).
* **Tools Required:**
  * **Wireshark** (`sudo apt install wireshark`)
  * **NetworkMiner** (Mono runtime on Kali or running on Windows)
  * **Microsoft Excel / LibreOffice Calc** (For interactive `.xlsx` ticketing)

---

## 📁 Repository Structure

```text
.
├── networkinvestigation2.pcap                     # Pre-captured network traffic file
├── CyberAttack_Incident_Ticket_Interactive_Final.xlsx # Interactive student incident ticket
└── README.md                                       # Lab instructions and step-by-step workflow
```

---

## 🚀 Step-by-Step Lab Execution Guide

### Step 1: Verify File Integrity & Workspace Setup

1. Open your Kali Linux terminal and navigate to your working directory:
   ```bash
   cd ~/Desktop
   ```
2. Verify the cryptographic hash of the provided capture file:
   ```bash
   sha256sum networkinvestigation2.pcap
   ```
3. Record the generated SHA-256 hash in your incident ticket report under technical details.

---

### Step 2: Protocol & Stream Analysis in Wireshark

1. Launch Wireshark from the Kali application menu or terminal:
   ```bash
   wireshark networkinvestigation2.pcap &
   ```
2. Apply essential display filters to inspect suspicious activity:
   * Filter for HTTP traffic:
     ```text
     http
     ```
   * Filter for HTTP GET requests containing parameters:
     ```text
     http.request.method == "GET"
     ```
   * Filter by target ports or IP addresses:
     ```text
     tcp.port == 8080 || ip.addr == 127.0.0.1
     ```
3. Right-click any suspicious HTTP packet and select **Follow -> HTTP Stream** to view the full request/response conversation in cleartext.

---

### Step 3: Artifact Extraction in NetworkMiner

1. Launch **NetworkMiner** on your system.
2. Go to **File -> Open** and load `networkinvestigation2.pcap`.
3. Systematically review the extracted network artifacts across tabs:
   * **Hosts Tab:** Identify target endpoints, operating systems, and MAC addresses.
   * **Parameters Tab:** Locate extracted HTTP query parameters (e.g., `module=...`, `id=...`).
   * **Sessions / Headers Tab:** Inspect custom user headers (e.g., `X-Audit-Status`, `X-Secret-Flag`, `User-Agent`).
   * **Files / Credentials Tabs:** Check for dropped payloads or plain-text authorization tokens.

---

### Step 4: Incident Ticket Completion

1. Open `CyberAttack_Incident_Ticket_Interactive_Final.xlsx` in Excel or LibreOffice Calc.
2. Fill out all technical metadata fields (Analyst Name, Date, File Hash, Target IPs, Protocols).
3. Use the embedded **Drop-Down Men Menus** to classify the incident:
   * **Severity Level:** (`Low`, `Medium`, `High`, `Critical`)
   * **Incident Type:** Select standard threats (e.g., `Phishing`, `Malware Infection`) or formal cyberattack vectors (e.g., `Command & Control (C2) Beaconing`, `Data Exfiltration`).
   * **Ticket Status & Mitigation Phase:** Map to the NIST Incident Response lifecycle (`Detection & Analysis`, `Containment & Eradication`, etc.).
   * **Action Item Statuses:** (`Pending`, `In Progress`, `Completed`).
4. Detail your forensic investigation summary, outlining extracted prank flags, suspicious endpoints, and recommended perimeter firewall blocking rules.

---

## 📤 Lab Submission Methods

Students must submit their completed work using one of the following two methods:

### Option 1: GitHub Issue Submission

1. Go to the **Issues** tab of this repository and click **New Issue**.
2. Title the issue: `[CTM-ACTIVITY-10] <Your Name>`.
3. Attach your completed `CyberAttack_Incident_Ticket_Interactive_Final.xlsx` spreadsheet file.
4. Upload screenshots showing:
   * Execution of `sha256sum networkinvestigation2.pcap` in the Kali terminal.
   * Wireshark window displaying filtered HTTP GET requests and TCP stream follow.
   * NetworkMiner window highlighting the **Parameters** or **Sessions** tab showing extracted telemetry/prank flags.
5. Click **Submit New Issue**.

### Option 2: Pull Request (PR) Submission

1. Fork this repository to your personal GitHub account.
2. Create a submission directory in your fork named `submissions/`.
3. Place your completed `CyberAttack_Incident_Ticket_Interactive_Final.xlsx` and analysis screenshots inside `submissions/`.
4. Commit your changes and push them to your repository fork.
5. Create a Pull Request back to the main repository titled: `Submission: Activity 10 - <Your Name>`.
