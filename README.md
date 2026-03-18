# Azure AD Honeypot SIEM Project (Microsoft Sentinel)

## 🧠 Executive Summary
This project simulates a real-world Security Operations Center (SOC) scenario by deploying a deliberately vulnerable Windows-based virtual machine in Microsoft Azure to act as a honeypot. The system was exposed to the public internet via RDP (port 3389) to attract malicious activity.

Logs were ingested into Microsoft Sentinel using the Azure Monitor Agent, where security events (specifically Event ID 4625 – failed login attempts) were analyzed to identify brute-force attacks, username enumeration, and attacker behavior patterns across multiple regions and hosting providers.

---

## 🏗️ Architecture Overview
- **Cloud Platform:** Microsoft Azure  
- **Virtual Machine:** Windows 10 (Honeypot)  
- **SIEM:** Microsoft Sentinel  
- **Log Ingestion:** Azure Monitor Agent (AMA)  
- **Log Source:** Windows Security Events  
- **Attack Vector:** Public RDP Exposure (3389)  

### 🔁 Data Flow
1. Public internet → RDP brute force attempts  
2. Windows VM logs security events  
3. Azure Monitor Agent collects logs  
4. Logs sent to Log Analytics Workspace  
5. Microsoft Sentinel ingests and analyzes data  

---

## 🚨 Honeypot Configuration
The virtual machine was intentionally configured with:
- Public IP address
- Open RDP port (3389) to all IP addresses
- Minimal security hardening

> ⚠️ This configuration is intentionally insecure and should **never** be used in production environments.

This setup allows attackers to:
- Attempt credential-based attacks
- Enumerate usernames
- Perform automated brute-force attempts

---

## 📊 Log Collection & SIEM Integration
- Configured **Log Analytics Workspace**
- Enabled **Microsoft Sentinel**
- Installed **Azure Monitor Agent (AMA)**
- Connected **Windows Security Events via AMA**

### Key Event Monitored:
- **Event ID 4625** → Failed login attempts

---

## 🔍 Attack Analysis

### 📈 Attack Volume
Over a **3-day period**, the honeypot captured:
- **30,000+ login attempts from a single source**
- Multiple additional sources with thousands of attempts
- Continuous attack patterns indicating automation

---

### 🌍 Geographic Distribution of Attacks
![Geographic Attack Map](./images/Geographic_distribution_map.png)

> 📌 This visualization (created in Tableau) highlights global attack sources, showing concentration in specific regions.

---

### 🏢 Top Hosting Providers Used by Attackers
![Attack Source Providers](./images/top_company_hosting_attackers.png)

> 📌 This chart shows the most common hosting providers used in attack attempts, indicating likely use of VPS infrastructure and botnets.

---

### 🧨 Observed Attack Techniques

#### 1. Brute Force Attacks (MITRE T1110)
- High-frequency login attempts
- Thousands of repeated authentication failures
- Automated attack behavior

#### 2. Username Enumeration
Attackers attempted common and service-based usernames:
- Administrator, Admin, Root  
- SQLServer, FTP, Support  
- Business roles: HR, Manager, Accounting  

#### 3. Credential Spraying
- Large sets of usernames tested with repeated attempts
- Indicates use of known credential lists

#### 4. Global Attack Patterns
- Usernames in multiple languages
- Suggests distributed attack infrastructure

---

## 🧪 Sample Log Data
Example of captured event:
Event ID: 4625
Message: An account failed to log on
Source: Remote IP
Status: Failure

---

## 🧠 MITRE ATT&CK Mapping
| Technique | ID | Description |
|----------|----|------------|
| Brute Force | T1110 | Repeated login attempts |
| Valid Accounts | T1078 | Attempted use of common credentials |
| Credential Access | TA0006 | Targeting authentication systems |

---

## 📌 Key Findings
- Attackers begin targeting exposed systems within minutes
- Majority of traffic is automated (bot-driven)
- Common credential lists are widely reused
- Cloud-hosted infrastructure is frequently used for attacks
- Persistent attack attempts occur over multiple days

---

## 🔐 Security Recommendations
Based on findings:

- Disable public RDP access  
- Implement Multi-Factor Authentication (MFA)  
- Use Network Security Groups (NSGs) with IP restrictions  
- Enable account lockout policies  
- Monitor logs with a SIEM (e.g., Sentinel)  
- Use Just-In-Time (JIT) VM access  

---

azure-ad-honeypot-siem-analysis/
├── data/
│   ├── honeypot_attack_data.xlsx        # Raw exported log data from Sentinel
│   └── cleaned_attack_summary.csv       # Aggregated attack analysis dataset
├── images/
│   ├── geo-map.png                     # Geographic distribution of attacks (Tableau)
│   └── attack-bar.png                  # Top attacker hosting providers (Tableau)
├── queries/
│   └── failed_logins.kql               # KQL query for Event ID 4625 analysis
├── documentation/
│   └── setup_notes.md                  # (Optional) Step-by-step lab setup notes
├── README.md                           # Project overview and analysis
└── LICENSE

---

## 🛠️ Tools & Technologies Used
- Microsoft Azure  
- Microsoft Sentinel (SIEM)  
- Azure Monitor Agent (AMA)  
- Log Analytics Workspace  
- Windows Event Logs  
- Tableau (Data Visualization)  

---

## 🚀 Future Improvements
- Add real-time alerting rules in Sentinel  
- Implement automated response (SOAR)  
- Expand to Active Directory attack simulation  
- Correlate multiple event IDs (4624, 4672, etc.)  
- Integrate threat intelligence feeds  

---

## 📣 Author
Jeremy Gutierrez  
Aspiring Security Analyst | Network Security | SIEM & Threat Detection
