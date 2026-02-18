# Intrusion Detection Home Lab

## 📌 Objective
The purpose of this project was to architect a controlled, virtualized network environment to simulate advanced cyber attacks and practice real-time threat detection, incident response, and log analysis.

## 🏗️ Architecture & Tech Stack
* **Host Environment:** macOS (Apple M3)
* **Offensive Security Machine (Attacker):** Kali Linux
* **Target Machine (Victim):** Windows OS
* **SIEM / Log Aggregation:** Splunk Enterprise

## ⚙️ Setup & Configuration
1. **Virtualization:** Configured isolated virtual networks for the attacker and target machines to ensure safe execution of offensive maneuvers.
2. **Log Forwarding:** Configured the Windows target machine to forward security, system, and application event logs to the centralized Splunk indexer.
3. **SIEM Tuning:** Set up data inputs and extracted necessary fields within Splunk to ensure optimal parsing of Windows Event Logs.

## ⚔️ Simulated Attacks
* **Network Discovery:** Performed aggressive Nmap stealth scans to identify open ports and running services on the Windows target.
* **Brute Force:** Executed a dictionary attack using Hydra against remote desktop/SMB protocols.
* **Defense Evasion:** Simulated an attacker covering their tracks by wiping system and security logs.

---

## 🛡️ Splunk Threat Hunting & Detection
Below is a collection of Search Processing Language (SPL) queries I developed to detect the simulated attacks from my Kali Linux machine against the Windows target environment.

### 1. Detecting RDP/SMB Brute Force Attacks
* **Scenario:** The Kali machine attempts a dictionary attack using Hydra against the Windows machine to guess user credentials.
* **Log Source:** Windows Security Event Logs
* **Query:**
  ```spl
  index=windows sourcetype="XmlWinEventLog:Security" EventCode=4625 
  | stats count min(_time) as first_attempt max(_time) as last_attempt by TargetUserName, IpAddress, WorkstationName
  | where count > 10
  | convert ctime(first_attempt) ctime(last_attempt)
  | sort - count
