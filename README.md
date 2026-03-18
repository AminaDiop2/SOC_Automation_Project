## SOC Automation Project : AI-Integrated Incident Response
### Project Overview  
This project demonstrates an automated Security Operations Center (SOC) workflow that integrates **Splunk** (SIEM), **N8N** (SOAR/Automation), and **Google** **Gemini** (AI) to streamline incident analysis.

The system detects Windows brute-force login attempts (Event ID 4625), automatically sends the alert to an automation workflow, and uses AI to generate a structured security report and recommended response actions delivered directly to analysts in **Slack**.

This project demonstrates how AI can augment Tier 1 SOC analysts by reducing manual triage and improving response time

##

### Technical Architecture  
SIEM: **Splunk Enterprise**   
Automation/SOAR: **N8N** (Self-hosted via Docker)  
Endpoint: **Windows 10** (Target machine)  
AI Engine: **Google Gemini**  
Communication: **Slack**  
Windows Endpoint  (Failed logins using RDP)  
      │  
      │ Event Logs (4625)    
      ▼  
Splunk SIEM    
      │  
      │ Alert Webhook    
      ▼    
N8N Automation       
      │      
      │ AI Analysis    
      ▼  
Google Gemini    
      │  
      ▼  
Slack Alert Channel  

##

### Step-by-Step Implementation
#### Phase 1: Environment Setup
- Hypervisor: Installed VMware Workstation Pro to host the lab environment.  
- Virtual Machines:  
  * Windows 10: Configured as the target endpoint for log generation.  
  * Ubuntu Server (Splunk): Dedicated instance for Splunk Enterprise.  
  * Ubuntu Server (N8N): Dedicated instance for the automation engine.  
[View Documentation here](Documentation/Phase1)   
#### Phase 2: SIEM Configuration (Splunk)
- Splunk Installation: Installed Splunk Enterprise on the Ubuntu VM using the .deb package.    
- Telemetry Ingestion:  
  * Installed Splunk Universal Forwarder on the Windows 10 VM.
  * Configured inputs.conf to monitor Windows Security Event Logs (Event ID 4625 - Failed Logins).
  * Installed the Splunk Add-on for Microsoft Windows to normalize data.
- Alert Creation: Created a scheduled search in Splunk to detect failed login attempts and configured a Webhook trigger to send alert data to N8N .    
[View Documentation here](Documentation/Phase2) 
#### Phase 3: Automation Workflow (N8N)  
- Docker Deployment: Deployed N8N on Ubuntu using Docker Compose.   
- Webhook Integration: Created a Webhook node in N8N to receive the JSON payload from Splunk.    
- AI Analysis (Gemini): Integrated the OpenAI node using Gemini.  
- Provided a System Prompt to act as a Tier 1 SOC Analyst.  
- Instructed the AI to summarize the alert, map it to the MITRE ATT&CK framework, and suggest remediation steps.  
[View Documentation here](Documentation/Phase3) 
#### Phase 4: Notification (Slack)  
- Slack App: Created a custom Slack App and configured an OAuth Bot Token with chat:write permissions.  
- Final Output: Configured the Slack node in N8N to post the AI-generated security report into a dedicated #alerts channel.    
[View Documentation here](Documentation/Phase4) 
##

### Key Features
- Real-time Alerting: Immediate notification of suspicious activity.  
- AI-Powered Context: Automatically translates raw logs into human-readable security summaries.  
- Efficiency: Reduces the "mean time to respond" (MTTR) for Tier 1 analysts.  
### Lab Results
When a brute-force attack is simulated, the system successfully:  
1.Detects the high volume of Event ID 4625 logs with Splunk.
<img width="1681" height="698" alt="screen34" src="https://github.com/user-attachments/assets/f6168866-4772-467f-bfda-79a6b8ea86a1" />

2.Forwards the data to N8N through the Webhook on Splunk.
<img width="1388" height="833" alt="fixedn8n" src="https://github.com/user-attachments/assets/3e792023-23d9-4254-8aa2-1c62963a955a" />

3.Posts a Slack message detailing the attack source, the MITRE technique, and recommendations given by Gemini [View here]().
<img width="766" height="557" alt="final5" src="https://github.com/user-attachments/assets/9758d0da-8040-4396-b2e6-1db4fe30ae04" />


