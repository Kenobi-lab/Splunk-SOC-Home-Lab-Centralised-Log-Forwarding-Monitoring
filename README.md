
# Splunk SOC Home Lab – Centralised Log Forwarding & Monitoring

## 📌 Overview
This project demonstrates a **hands-on SOC-style Splunk lab** where logs from multiple operating systems are centrally collected, indexed, and analysed. The lab was designed to replicate a real-world Security Operations Centre (SOC) environment, focusing on **log ingestion, forwarder management, and data validation**.

The environment includes:
- A **Splunk Enterprise Indexer** running on Ubuntu
- **Universal Forwarders** on Kali Linux and Windows Server
- Centralised log collection over TCP (port 9997)

This lab highlights my practical experience with **SIEM deployment, log forwarding, troubleshooting ingestion issues, and validating security telemetry**.

---

## 🏗️ Lab Architecture

```
[Kali Linux] --------┐
                     ├──> [Ubuntu Splunk Enterprise Indexer]
[Windows Server] ----┘           (Port 9997)
```

### Roles
| System | Role |
|------|------|
| Ubuntu Server | Splunk Enterprise (Indexer & Receiver) |
| Kali Linux | Universal Forwarder |
| Windows Server | Universal Forwarder |

---

## ⚙️ Technologies Used
- Splunk Enterprise
- Splunk Universal Forwarder
- Linux (Ubuntu, Kali)
- Windows Server
- TCP Log Forwarding (9997)
- CLI-based Splunk Administration

---

## 🚀 Implementation Steps

### 1️⃣ Splunk Indexer (Ubuntu)
- Installed and configured Splunk Enterprise
- Enabled receiving on TCP port **9997**
- Verified listener using `netstat`
- Configured Splunk to start at boot
- Generated test logs on Ubuntu Linux

<img width="877" height="42" alt="Image" src="https://github.com/user-attachments/assets/fe2b0719-f128-4891-9899-2ef552adcaae" />

<img width="1638" height="217" alt="Image" src="https://github.com/user-attachments/assets/bab37d2e-44c2-404a-ba90-b00cb37f9add" />

<img width="715" height="52" alt="Image" src="https://github.com/user-attachments/assets/2e71de2c-2532-4075-896e-398202b0f396" />

<img width="1637" height="502" alt="Image" src="https://github.com/user-attachments/assets/e8660f3b-960e-4290-a7e2-d4ec32009541" />

**Key command:**
```bash
/opt/splunk/bin/splunk enable listen 9997
```

---

### 2️⃣ Kali Linux – Universal Forwarder
- Installed Splunk Universal Forwarder using `.tgz` package
- Created UF admin credentials
- Configured forwarding to Ubuntu indexer
- Monitored `/var/log` for system logs



**Key commands:**
```bash
splunk add forward-server <Indexer_IP>:9997
splunk add monitor /var/log
```

---

### 3️⃣ Windows Server – Universal Forwarder
- Installed Universal Forwarder (MSI)
- Configured forwarding to the same indexer
- Monitored Windows Event Logs and system directories

---

## 🔍 Validation & Testing

To confirm successful ingestion:
- Generated test logs on Kali Linux
- Verified logs appeared in Splunk Search
- Confirmed correct metadata:
  - Host
  - Source
  - Sourcetype

**Example indexed event:**
- Host: `kali`
- Source: `/var/log/test_splunk.log`
- Indexed in near real-time

---

## 🛠️ Troubleshooting Performed

During setup, several real-world issues were encountered and resolved:
- Permission errors with Splunk directories
- Forwarder session authentication issues
- Port connectivity validation
- Differentiating forwarder vs indexer CLI behaviour

This reinforced a strong understanding of **Splunk architecture and operational troubleshooting**.

---

## 📊 Skills Demonstrated
- SIEM deployment and configuration
- Log forwarding architecture
- Linux & Windows administration
- Network troubleshooting
- Security monitoring fundamentals
- SOC workflow understanding

---

## 📈 Next Enhancements
- Create separate indexes per host
- Add Windows Security Event Log monitoring
- Build SOC dashboards (failed logins, sudo activity)
- Integrate threat intelligence feeds
- Document detections and alerts

---

## 🧠 Key Takeaway
This lab demonstrates my ability to **design, deploy, and validate a working SIEM environment**, mirroring tasks expected of a **SOC Analyst** in production environments.

---

📂 *This project is part of my ongoing SOC home lab and continuous professional development in cybersecurity.*
