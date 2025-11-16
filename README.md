# 🟣 Windows Logon Monitoring — Splunk Dashboard  
A real-time monitoring dashboard for Windows Security Logon events using Splunk.  
This project helps visualize successful logons, failed logons, and detect brute-force attack attempts using Windows Security Event Logs (4624 & 4625).

---

## 📌 Features  
✔️ Monitor failed logon events (4625)  
✔️ Visualize successful logons (4624)  
✔️ Detect brute-force attempts automatically  
✔️ Easy-to-import Splunk XML dashboard  
✔️ Includes all SPL queries  
✔️ Lightweight and ideal for SOC, Blue Teams, & Home Labs  

---

## 📊 Dashboard Preview

### Dashboard Overview  
`screenshots/dashboard_overview.png`

### Failed Logons Chart  
`screenshots/failed_logons_chart.png`

### Successful Logons Chart  
`screenshots/successful_logons_chart.png`

### Raw Failed Logon Event  
`screenshots/raw_failed_logon_event.png`

---

## 🧠 SPL Queries

### 🔹 Failed Logons Over Time (4625)
```spl
index=* sourcetype=WinEventLog:Security EventCode=4625
| timechart span=1m count
🔹 Successful Logons Over Time (4624)
spl
Copy code
index=* sourcetype=WinEventLog:Security EventCode=4624
| timechart span=1m count
🔥 Brute Force Detection (5+ failures in 2 mins)
spl
Copy code
index=* sourcetype=WinEventLog:Security EventCode=4625
| bin _time span=2m
| stats count by Account_Name, Source_Network_Address, _time
| where count >= 5
| sort - count
📥 Importing the Dashboard into Splunk
Open Splunk → Search & Reporting

Go to Dashboards

Click Create New Dashboard

Choose Source mode

Paste all content from dashboard.xml

Save → Dashboard loads immediately ✔️

📁 Repository Structure
markdown
Copy code
windows-logon-monitoring-splunk/
│
├── dashboard.xml
├── README.md
├── SPL_queries.txt
│
└── screenshots/
       ├── dashboard_overview.png
       ├── failed_logons_chart.png
       ├── successful_logons_chart.png
       └── raw_failed_logon_event.png
🚀 Requirements
Splunk Enterprise or Splunk Free

Windows Security Event Logs enabled

Input configured:

ruby
Copy code
WinEventLog://Security
🛡️ Use Cases
SOC Analyst / Blue Team lab

Detect password spraying / brute-force attacks

Monitor compromised accounts

Windows security visibility for training

👨‍💻 Author
Sathish
SOC Analyst | Cybersecurity Enthusiast

