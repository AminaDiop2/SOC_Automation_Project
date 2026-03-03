## SOC Automation Project : AI-Integrated Incident Response
### Project Overview  
This project demonstrates an automated SOC workflow that integrates Splunk (SIEM), N8N (Automation Platform), and Gemini(Google) to streamline incident analysis. The workflow detects brute-force attempts on a Windows endpoint, and uses AI to provide a structured summary and recommended actions to analysts in Slack.

##

### Technical Architecture  
SIEM: Splunk Enterprise  
Automation/SOAR: N8N (Self-hosted via Docker)  
Endpoint: Windows 10 (Target machine)  
AI Engine: Gemini  
Communication: Slack  

##

### Step-by-Step Implementation
#### Phase 1: Environment Setup
Hypervisor: Installed VMware Workstation Pro to host the lab environment.  
Virtual Machines:  
Windows 10: Configured as the target endpoint for log generation[View here]().  
Ubuntu Server (Splunk): Dedicated instance for Splunk Enterprise [View here]().  
Ubuntu Server (N8N): Dedicated instance for the automation engine [View here]().  
Kali Linux (Optional): Used for simulating attacks.  
#### Phase 2: SIEM Configuration (Splunk)
Splunk Installation:   
Installed Splunk Enterprise on the Ubuntu VM using the .deb package [View here]().    
Telemetry Ingestion:  
Installed Splunk Universal Forwarder on the Windows 10 VM[View here]().
Configured inputs.conf to monitor Windows Security Event Logs (Event ID 4625 - Failed Logins).
Installed the Splunk Add-on for Microsoft Windows to normalize data.
Alert Creation: Created a scheduled search in Splunk to detect failed login attempts and configured a Webhook trigger to send alert data to N8N [View here]().
#### Phase 3: Automation Workflow (N8N)  
Docker Deployment: Deployed N8N on Ubuntu using Docker Compose [View here]().   
Webhook Integration: Created a Webhook node in N8N to receive the JSON payload from Splunk [View here]().   
Threat Intel Enrichment: Added an HTTP Request node to query the AbuseIPDB API. This checks the reputation of the source IP address found in the Splunk alert [View here]().  
AI Analysis (Gemini): Integrated the OpenAI node using Gemini.  
Provided a System Prompt to act as a Tier 1 SOC Analyst [View here]().  
Instructed the AI to summarize the alert, map it to the MITRE ATT&CK framework, and suggest remediation steps [View here]().  
#### Phase 4: Notification (Slack)  
Slack App: Created a custom Slack App and configured an OAuth Bot Token with chat:write permissions [View here]().  
Final Output: Configured the Slack node in N8N to post the AI-generated security report into a dedicated #alerts channel [View here]().  

##

### Key Features
Real-time Alerting: Immediate notification of suspicious activity.  
AI-Powered Context: Automatically translates raw logs into human-readable security summaries.  
Efficiency: Reduces the "mean time to respond" (MTTR) for Tier 1 analysts.  
### Lab Results
When a brute-force attack is simulated, the system successfully:  
1.Detects the high volume of Event ID 4625 logs.  
2.Forwards the data to N8N.    
3.Posts a Slack message detailing the attack source (e.g., Romania), the MITRE technique (T1110 - Brute Force), and recommending an IP block [View here]().

