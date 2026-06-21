# 🛡️ Agentic AI for Security

> A hands-on masterclass project building an AI-powered SOC automation system — integrating Wazuh SIEM, n8n workflow orchestration, the Claude API, Postman, and a full VMware attack/defense homelab — from zero to a working AI Threat Hunter Agent.

---

## 📌 Overview

This project follows a structured 10-lesson masterclass (by [Atlantium AI](https://atlantiumai.io)) covering the full lifecycle of building an **Agentic AI Security Operations Center**:

- Spinning up a multi-VM homelab with Wazuh and n8n
- Simulating real attacks using Atomic Red Team and offensive tools from Kali
- Ingesting and monitoring logs with auditd, Sysmon, and Apache
- Exploring the Wazuh REST API with Postman
- Building and iterating on an AI Agent that autonomously triages EDR alerts
- Running a full attack chain (recon → pivot → exploit → privesc) to feed the AI Threat Hunter
- Benchmarking LLMs (Claude, Gemini, GPT) as the AI reasoning engine

---

## 📚 Masterclass Curriculum

| #   |            Title                                             |                    Key Topics                                                |
|-----|--------------------------------------------------------------|------------------------------------------------------------------------------|
| 0   | Lab Setup for Agentic AI Security Automation                 | VMware VMs, Docker, Wazuh + n8n deployment, VM tools, static IPs             |
| 1   | Wazuh + n8n Architecture & Attack Simulation                 | Architecture overview, Wazuh agent deployment, first attack simulation       |
| 2   | Auditd + Wazuh Integration — Atomic Red Team                 | Auditd install & rules, ossec.conf config, Atomic Red Team via PowerShell    |
| 3   | Exploring the Wazuh API with Postman                         | REST API auth, alert queries, Postman collections, API-driven hunting        |
| 4   | Building an AI Cybersecurity Agent with n8n                  | First n8n AI Agent node, Wazuh API integration, agent workflow wiring        |
| 5   | Build an EDR Alert Triage AI Agent                           | Alert ingestion, severity filtering, AI triage, MITRE ATT&CK mapping         |
| 5.5 | Enhancing the Lab — Prep for AI Threat Hunter                | Vulnerable web server setup, Remmina RDP, lab hardening, new attack surfaces |
| 5.6 | Installing Wazuh Agents, Auditd & Sysmon                     | Agent deployment across VMs, Sysmon on Windows, auditd on Linux targets      |
| 6   | Full Attack Chain — Recon, Pivoting, Exploitation & Priv-Esc | nmap, Hydra, proxychains, nikto, gospider, ffuf, reverse shell, SUID privesc |
| 7   | Building AI Threat Hunter Agent 1.0 + LLM Battle             | Threat Hunter Agent build, Claude vs Gemini vs GPT-5 Mini benchmark          |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   VMware Homelab                        │
│                                                         │
│  [Kali Linux] ──attack──► [Ubuntu Web Server]           │
│       │                   [Windows 11]                  │
│       │                         │                       │
│       │              Wazuh Agents (logs)                │
│       │                         │                       │
│       └──────────────► [Ubuntu AI - Wazuh Docker]       │
│                              │                          │
│                         REST API                        │
│                              │                          │
│                        [n8n Engine]                     │
│                              │                          │
│              ┌───────────────┼──────────────┐           │
│              ▼               ▼              ▼           │
│        Claude API       Gemini API      GPT API         │
│     (Threat Hunter)    (LLM Battle)  (LLM Battle)       │
│              │                                          │
│              ▼                                          │
│       SOC Analyst Report                                │
└─────────────────────────────────────────────────────────┘
```

---

## 🧰 Tech Stack

|        Tool                |                     Role                                            |
|----------------------------|---------------------------------------------------------------------|
| **Wazuh** (Docker)         | SIEM — alert generation, log ingestion, threat detection            |
| **n8n**                    | Workflow automation and AI Agent orchestration                      |
| **Claude API** (Anthropic) | Primary AI reasoning — triage, threat hunting, report drafting      |
| **Gemini API** (Google)    | LLM benchmarking and alternative reasoning engine                   |
| **GPT** (OpenAI)           | LLM benchmarking (Lesson 7 battle)                                  |
| **Postman**                | REST API testing — Wazuh API & n8n webhook validation               |
| **Docker**                 | Container runtime for Wazuh single-node stack                       |
| **Ubuntu AI (VM)**         | Host for Wazuh (Docker) + n8n — SIEM & automation engine            |
| **Ubuntu Web Server (VM)** | Vulnerable web app target — attack simulation (nikto, ffuf, RCE)    |
| **Kali Linux (VM)**        | Attacker machine — full offensive toolkit                           |
| **Windows 11 (VM)**        | Endpoint target — Wazuh agent + Sysmon monitoring                   |
| **Atomic Red Team**        | Adversary simulation framework (MITRE ATT&CK mapped)                |
| **Auditd**                 | Linux kernel-level audit logging for privilege escalation detection |
| **Sysmon**                 | Windows process and network telemetry for EDR visibility            |

---

## ✨ Features

- ✅ Full multi-VM homelab with attacker, defender, and target systems
- ✅ Wazuh SIEM deployed via Docker with single-node stack
- ✅ Wazuh agents on Linux and Windows endpoints
- ✅ Auditd rules for SUID abuse, root file access, and privilege escalation
- ✅ Sysmon telemetry on Windows endpoint
- ✅ Atomic Red Team attack simulation mapped to MITRE ATT&CK
- ✅ Full attack chain execution (recon → pivot → exploit → privesc)
- ✅ Wazuh API explored and documented via Postman collections
- ✅ n8n AI Agent for automated EDR alert triage
- ✅ AI-driven severity classification and MITRE ATT&CK mapping
- ✅ AI Threat Hunter Agent 1.0 built and tested
- ✅ LLM benchmark: Claude vs Gemini vs GPT on real security alerts

---

## 📁 Project Structure

```
agentic-ai-for-security/
├── n8n/
│   ├── edr-triage-agent.json          # Lesson 5 — EDR Alert Triage workflow
│   ├── threat-hunter-agent-v1.json    # Lesson 7 — AI Threat Hunter Agent 1.0
│   └── README.md
├── postman/
│   ├── wazuh-api-collection.json      # Wazuh REST API collection
│   ├── n8n-webhooks-collection.json   # n8n webhook test collection
│   └── environment-template.json      # Variable template (no real creds)
├── wazuh/
│   └── docker-compose.yml             # Wazuh single-node Docker config
├── audit-rules/
│   └── priv_esc.rules                 # Custom auditd rules for privesc detection
├── docs/
│   ├── architecture-diagram.png
│   └── sample-soc-report.md           # Example AI-generated SOC report
├── .env.example
├── .gitignore
└── README.md
```

---

## ⚙️ Setup & Installation

### Prerequisites

- VMware Workstation (or equivalent hypervisor)
- Docker & Docker Compose
- n8n (self-hosted or cloud)
- Anthropic API key
- Postman

### 1. Clone the Lab Repository

```bash
git clone https://github.com/Atlantium-AI/wazuh-n8n-lab-setup.git
cd wazuh-n8n-lab-setup
```

### 2. Install Docker & Spin Up Wazuh + n8n

```bash
# Install Docker
sudo ./install-docker.sh

# Deploy all containers (Wazuh + n8n)
sudo ./docker-spin-up.sh

# Verify containers are running
sudo docker ps

# To stop containers
sudo docker compose down

# To restart existing containers
sudo docker compose up -d
```

### 3. Install VM Tools (clipboard support)

```bash
sudo apt install open-vm-tools open-vm-tools-desktop -y
sudo systemctl restart vmtoolsd
```

### 4. Update & Install Git

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git -y
```

### 5. Deploy Wazuh Agent (on target VMs)

**Ubuntu:**
```bash
# Run the install command generated from the Wazuh dashboard
sudo wget <agent-install-command>

# Enable and start the agent
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
sudo systemctl status wazuh-agent --no-pager
```

**Windows (PowerShell — Run as Administrator):**
```powershell
# Run the install command generated from the Wazuh dashboard
Invoke-WebRequest -Uri <agent-install-command> -OutFile wazuh-agent.msi
.\wazuh-agent.msi /q WAZUH_MANAGER="<wazuh-manager-ip>"

# Start the Wazuh service
NET START WazuhSvc
```

### 6. Configure Environment Variables

```bash
cp .env.example .env
```

```env
CLAUDE_API_KEY=your_anthropic_api_key
WAZUH_API_URL=https://your-wazuh-host:55000
WAZUH_USER=your_wazuh_user
WAZUH_PASS=your_wazuh_password
N8N_WEBHOOK_URL=https://your-n8n-instance/webhook/soc-agent
```

### 7. Import n8n Workflows

1. Open your n8n instance
2. **Workflows** → **Import from file**
3. Import files from the `/n8n` folder
4. Update Wazuh and Claude API credentials in each node
5. Activate the workflow

### 8. Import Postman Collections

```bash
git pull
sudo ./install-postman.sh
```

1. Postman → **Import** → select `/postman` files
2. Configure environment using `environment-template.json`
3. Run collections to validate all endpoints

---

## 📊 Log Sources Monitored

|        Log File                        |  Type  |             What It Detects                         |
|----------------------------------------|--------|-----------------------------------------------------|
| `/var/log/auth.log`                    | syslog | SSH brute force, sudo abuse, login failures         |
| `/var/log/apache2/access.log`          | apache | Web scans, RCE attempts, directory traversal        |
| `/var/log/apache2/error.log`           | apache | Server-side errors from exploitation attempts       |
| `/var/log/syslog`                      | syslog | General system events                               |
| `/var/log/audit/audit.log`             | audit  | SUID abuse, root file reads, privilege escalation   |
| `Microsoft-Windows-Sysmon/Operational` | Sysmon | Process creation, network connections, file changes |

### Wazuh ossec.conf Log Sources Added

```xml
<localfile>
  <location>/var/log/auth.log</location>
  <log_format>syslog</log_format>
</localfile>

<localfile>
  <location>/var/log/apache2/access.log</location>
  <log_format>apache</log_format>
</localfile>

<localfile>
  <location>/var/log/apache2/error.log</location>
  <log_format>apache</log_format>
</localfile>

<localfile>
  <location>/var/log/audit/audit.log</location>
  <log_format>audit</log_format>
</localfile>
```

### Custom Auditd Rules (Privilege Escalation Detection)

```bash
# Install auditd
sudo apt install -y auditd audispd-plugins
sudo systemctl enable --now auditd
sudo systemctl start auditd

# Rules at /etc/audit/rules.d/priv_esc.rules
-a always,exit -F path=/usr/bin/python3 -F perm=x -F auid>=1000 -F auid!=4294967295 -k suid_python3
-a always,exit -F dir=/root -F perm=r -F auid>=1000 -F auid!=4294967295 -k read_root
-w /root/flag.txt -p rwxa -k read_flag

# Apply rules and restart
sudo augenrules --load
sudo systemctl restart auditd
sudo systemctl restart wazuh-agent
```

---

## ⚔️ Attack Simulation

### Atomic Red Team (MITRE ATT&CK Simulation)

```bash
# Install PowerShell
sudo apt install -y wget apt-transport-https software-properties-common gnupg git ca-certificates lsb-release
wget -q "https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb"
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
sudo apt update
sudo snap install powershell --classic

# Install Invoke-AtomicRedTeam
sudo pwsh -Command 'Install-Module -Name Invoke-AtomicRedTeam,powershell-yaml -Scope AllUsers -Force; Import-Module Invoke-AtomicRedTeam -Force; Write-Output "Installed+Imported"'

# Clone Atomic Red Team atomics
sudo git clone https://github.com/redcanaryco/atomic-red-team.git /opt/atomic-red-team

# Run all tests (⚠️ isolated lab environment only)
sudo pwsh -Command 'Import-Module Invoke-AtomicRedTeam; Invoke-AtomicTest All -PathToAtomicsFolder /opt/atomic-red-team/atomics -Cleanup -Confirm:$false'
```

### Full Attack Chain — Lesson 6 (from Kali)

```bash
# Reconnaissance
nmap -sT -sV -sC -Pn <target-ip>

# Brute force RDP
hydra -l <user> -P ShortPassList.txt rdp://<target-ip>

# SSH tunnel + proxychains pivot
ssh -D 9050 <user>@<target-ip> -fN
proxychains nmap -sn <subnet>/24 --open
proxychains nmap -sT -sV -sC -Pn <target-ip>

# Web vulnerability scanning
proxychains nikto -h <target-ip> -port 80

# Web crawling
sudo apt install gospider -y
proxychains gospider -s http://<target-ip> -d 5 -t 20 -o output/

# Parameter fuzzing (find RCE endpoint)
sudo apt install seclists -y
proxychains ffuf -u "http://<target-ip>/dynamic_cmd.php?FUZZ=whoami" \
     -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt \
     -mc 200,500

proxychains ffuf -u "http://<target-ip>/dynamic_cmd.php?FUZZ=whoami" \
     -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt \
     -mc 200,500 -fs 1057
```

### Vulnerable Web Server Setup (Ubuntu Web Server VM)

```bash
# Clone lab repo and set up vulnerable server
git clone https://github.com/Atlantium-AI/wazuh-n8n-lab-setup.git
chmod +x vulnerable-server.sh
./vulnerable-server.sh

# Set SUID on python3 (privesc target)
sudo su
chown root:root /usr/bin/python3
chmod 4755 /usr/bin/python3

# Plant flag
echo "flagName1288" | sudo tee flag.txt
```

---

## 🗺️ Homelab Environment

Built and tested in VMware Workstation:

|      VM           |      OS      |               Role                |    IP (VMnet8)     |
|-------------------|--------------|-----------------------------------|--------------------|
| Ubuntu AI         | Ubuntu 22.04 | Wazuh (Docker) + n8n              | 192.168.x.20       |
| Kali Linux        | Kali Linux   | Attacker — full offensive toolkit | 192.168.x.130      |
| Ubuntu Web Server | Ubuntu 22.04 | Vulnerable web app target         | 192.168.x.139      |
| Windows 11        | Windows 11   | Endpoint — Wazuh agent + Sysmon   | 192.168.x.128      |

**Useful tips:**
- `Ctrl + Alt` — release mouse pointer from VM
- Forgot Wazuh password: `cat wazuh-docker/single-node/docker-compose.yml`
- Check Wazuh containers: `sudo docker ps`

---

## 🤖 AI Threat Hunter Agent — Lesson 7

The final lesson builds **Threat Hunter Agent 1.0** in n8n and benchmarks three LLMs against real security alerts from the homelab:

|     LLM        | Provider  |          Notes                           |
|----------------|-----------|------------------------------------------|
| **Claude**     | Anthropic | Primary reasoning engine used throughout |
| **Gemini**     | Google    | Benchmarked in Lesson 7 LLM battle       |
| **GPT-5 Mini** | OpenAI    | Benchmarked in Lesson 7 LLM battle       |

The agent autonomously queries the Wazuh API, retrieves active alerts, reasons about the threat context, and produces structured analyst reports — with no manual intervention.

---

## 📬 Postman Collections

|           Collection           |             Description                         |
|--------------------------------|-------------------------------------------------|
| `wazuh-api-collection.json`    | Auth, alert queries, agent management           |
| `n8n-webhooks-collection.json` | Trigger and test SOC agent workflows            |
| `environment-template.json`    | Placeholder variables (safe for public sharing) |

**Wazuh Indexer Direct Query:**
```
https://single-node-wazuh.indexer-1:9200/wazuh-alerts-*/_search
```

---

## 🔐 Security Notes

- **Never commit real credentials** — use `.env` files and n8n credential store
- `.gitignore` excludes all `.env` files and Postman environments with real values
- All attack simulations were performed in an **isolated lab environment only**
- Lab VMs run on a private VMnet — no exposure to production or external networks

---

## 🛣️ Roadmap

| Phase | Feature | Status |
|-------|---------|--------|
| v0.1 | Multi-VM homelab setup (Wazuh + n8n + Kali + Windows) | ✅ Complete |
| v0.2 | Wazuh agent deployment on Linux and Windows endpoints | ✅ Complete |
| v0.3 | Auditd rules + Sysmon telemetry integration | ✅ Complete |
| v0.4 | Wazuh REST API exploration via Postman | ✅ Complete |
| v0.5 | n8n AI Agent — EDR alert triage workflow | ✅ Complete |
| v0.6 | Full attack chain execution (recon → pivot → exploit → privesc) | ✅ Complete |
| v0.7 | AI Threat Hunter Agent 1.0 build | ✅ Complete |
| v0.8 | LLM benchmark — Claude vs Gemini vs GPT | ✅ Complete |
| v0.9 | Automated response playbooks (isolate host, block IP) | ✅ Complete |
| v0.9 | Slack/email notification for high-severity alerts | ✅ Complete |
| v1.0 | Threat Hunter Agent 2.0 with memory and multi-step reasoning | 🔲 Future |
| v1.1 | VirusTotal API integration for IOC enrichment | 🔲 Future |
| v1.2 | Export threat hunt findings to MISP | 🔲 Future |
| v1.3 | GhostNet + NullByte unified risk dashboard | 🔲 Future |

---

## 👤 Author

**Eliezer Fuentes** — Cybersecurity Professional  
Threat Hunting | Vulnerability Management | SOC Automation | Offensive Security

[![GitHub](https://img.shields.io/badge/GitHub-enak223-181717?style=flat&logo=github)](https://github.com/enak223)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-eliezerfuentes-0A66C2?style=flat&logo=linkedin)](https://www.linkedin.com/in/eliezerfuentes/)

---

## 📄 License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

*Based on the Agentic AI for Security Masterclass by [Atlantium AI](https://atlantiumai.io)*

---

> *"The best SOC analyst isn't the one who waits for alerts — it's the one who builds the system that never sleeps."*
