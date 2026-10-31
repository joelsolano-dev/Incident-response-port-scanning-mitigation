# Case Study: Network Reconnaissance and Port Scanning Detection & Mitigation

## Overview
- **Incident Type:** Active Scanning / Port Scanning (MITRE ATT&CK T1595)
- **Environment:** Kali Linux
- **Objective:** Detect unauthorized reconnaissance traffic, analyze indicators of compromise, apply perimeter containment using UFW, and audit the mitigation effectiveness.

---

## Step 0 & 1: Simulation & Detection
Execution of an active TCP SYN scan (`nmap`) to map open services on the target architecture, followed by traffic triage.

![Simulation and Detection Evidence](./path-to-image-1.png)

---

## Step 2: IoC Analysis & Metrics
- **Attacker IP:** `127.0.0.1` (Controlled Lab Environment)
- **Attack Vector:** TCP SYN Half-Open Scanning (T1595)
- **Impact Assessment:** 1,000 ports probed within fraction-of-a-second intervals, targeting service exposure (SSH port 22).

---

## Step 3: Containment & Mitigation
Application of active perimeter defense rules via UFW to drop incoming packets originating from the hostile source IP.

![Firewall Containment Rule Evidence](./path-to-image-2.png)

---

## Step 4: Verification & Post-Mitigation Audit
Re-evaluation of target responsiveness following rule enforcement to validate successful threat neutralization.

![Post-Mitigation Audit Evidence](./path-to-image-3.png)
