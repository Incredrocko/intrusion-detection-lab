# Intrusion Detection Home Lab

## 📌 Objective
The purpose of this project was to architect a controlled, virtualized network environment to simulate advanced cyber attacks and practice real-time threat detection, incident response, and log analysis.

## 🏗️ Architecture & Tech Stack
* **Host Environment:** macOS (Apple M3 Silicon)
* **Offensive Security Machine (Attacker):** Kali Linux
* **Target Machine (Victim):** Windows OS
* **SIEM / Log Aggregation:** Splunk Enterprise

## ⚙️ Setup & Configuration
1. **Virtualization:** Configured isolated virtual networks for the attacker and target machines to ensure safe execution of offensive maneuvers.
2. **Log Forwarding:** Configured the Windows target machine to forward security, system, and application event logs to the centralized Splunk indexer.
3. **SIEM Tuning:** Set up data inputs and extracted necessary fields within Splunk to ensure optimal parsing of Windows Event Logs.

## ⚔️ Simulated Attacks
* **Network Discovery:** Performed aggressive Nmap stealth scans to identify open ports and running services on the Windows target.
* **Brute Force:** Executed a dictionary attack using Hydra against remote desktop protocols.

## 🛡️ Detection & Analysis
* Utilized Splunk Search Processing Language (SPL) to correlate failed login attempts and detect the brute force attack.
* Configured real-time alerts for anomalous process executions and unauthorized network connections.
* Successfully identified the exact timestamp, source IP, and methodology of the simulated breaches.
