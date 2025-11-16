# 🟣 Windows Logon Monitoring — Splunk Dashboard  
A real-time monitoring dashboard for Windows Security Logon events using Splunk.  
This dashboard visualizes successful logons, failed logons, and brute-force attack attempts.

---

## 📌 Features
✔️ Monitor failed logon events (4625)  
✔️ Visualize successful logons (4624)  
✔️ Detect brute-force attempts automatically  
✔️ Easy-to-import Splunk XML dashboard  
✔️ Includes all SPL queries  
✔️ Lightweight and ideal for SOC, Blue Teams, Home Labs  

---

## 📊 Dashboard Preview

### Dashboard Overview
`screenshot\dashboard_overview.png`
### Failed Logons Chart
`screenshot\failed_logons_chart.png`

### Successful Logons Chart
`screenshots\successful_logons_chart.png`

### Brute force chart
`screenshots\Brute_force.png`

---

## 🧠 SPL Queries

### 🔹 Failed Logons Over Time (4625)
```spl
index=* sourcetype=WinEventLog:Security EventCode=4625
| timechart span=1m count

####🔹 Successful Logons Over Time (4624)
```spl
index=* sourcetype=WinEventLog:Security EventCode=4624
| timechart span=1m count

####🔹Brute Force Detection (5+ failures in 2 mins)
```spl
index=* sourcetype=WinEventLog:Security EventCode=4625
| bin _time span=2m
| stats count by Account_Name, Source_Network_Address, _time
| where count >= 5
| sort - count

🚀 Requirements
1.Splunk Enterprise or Splunk Free

2.Windows Security Event Logs

3.Input enabled:WinEventLog://Security

🛡️ Use Cases
1.SOC Analyst / Blue Team Lab

2.Detect password spraying & brute-force attacks

3.Monitor compromised accounts

4. security visibility for home labs


👨‍💻 Author

Sathish
SOC Analyst | Cybersecurity Enthusiast


