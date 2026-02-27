# SOC_Automation_Project

🔐 SOC Automation Project 2.0 – AI-Enhanced SOC Workflow  
📌 Overview  
This project simulates a modern Security Operations Center (SOC) environment and demonstrates how automation and AI can improve alert triage, enrichment, and response workflows.
The lab integrates a SIEM platform, automation/orchestration tooling, and AI-driven analysis to replicate real-world SOC processes while reducing manual effort and alert fatigue.

---

🎯 Objectives  
Simulate real-world SOC alert generation and detection
Automate Tier 1 alert triage tasks
Enrich alerts with contextual threat intelligence
Use AI to assist in alert analysis and decision-making
Improve response time through automated workflows

---

🛠️ Tools & Technologies Used  
SIEM Platform (Splunk) – Log ingestion, searching, and alerting    
SOAR / Automation (n8n) – Workflow orchestration    
AI Integration – Automated alert summarization & analysis  
Windows/Linux Virtual Machines(VMware) – Endpoint log generation  
Sysmon – Advanced Windows logging  
Email/Notification System – Alert escalation  

---

🏗️ Lab Architecture  
Endpoint generates logs (Sysmon / Security logs)  
Logs are ingested into SIEM  
Detection rule triggers an alert  
Alert is forwarded to automation platform  
Automation workflow:  
Parses alert data    
Enriches indicators (IP/domain/hash)  
Sends data to AI for summarization  
Determines severity  
Sends notification / creates case  

---

🔍 Key Features    
✅ Automated Alert Triage  
Reduces manual SOC workload by automatically parsing and analyzing alerts.  
✅ Threat Intelligence Enrichment  
Extracts IOCs (IPs, hashes, domains) and enriches them for additional context.  
✅ AI-Powered Analysis   
Uses AI to:  
Summarize alerts  
Recommend next steps  
Classify severity  
✅ End-to-End Workflow Automation  
Demonstrates how SIEM and SOAR platforms integrate in a real SOC environment.  
