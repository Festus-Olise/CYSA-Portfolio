# 🚀 Wazuh SIEM Lab: Installation, Troubleshooting & Recovery

**Author:** Festus Olise  
**Date:** October 2025  
**Environment:** Ubuntu VM (VirtualBox), Wazuh 4.13

---

## 🧩 Overview

This lab documents my hands-on experience installing and troubleshooting the Wazuh SIEM stack on an Ubuntu VM. After a failed initial install, I performed a full recovery and now have a functional dashboard ready for agent deployment and log ingestion.

---

## 🛠️ Environment Setup

- **VM Name:** `Ubuntu_SOC`
- **Snapshot (Pre-Install):** `Ubuntu_SOC (Pre Wazuh Clean State)`
- **OS:** Ubuntu 22.04 LTS
- **Virtualization:** VirtualBox
- **Network:** Bridged Adapter

---

## 📦 Wazuh Installation Steps

```bash
curl -sO https://packages.wazuh.com/4.13/wazuh-install.sh
sudo bash ./wazuh-install.sh -a
```

This installs:
- Wazuh Manager
- Wazuh Indexer (OpenSearch)
- Wazuh Dashboard
Auto-generated credentials are stored in wazuh-install-files.tar.
To extract credentials:

```bash
sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
```
---
🔐 Dashboard Access
- URL: https://<VM_IP>
- Username: admin
- Password: from wazuh-passwords.txt
- Note: Accept self-signed certificate warning
---
🧵 Troubleshooting Summary (First Attempt)
- During my first attempt, I encountered several issues:
- Missing securityconfig/ files caused securityadmin.sh to fail
- Dashboard and API users were mismatched
- Manual recovery involved:
- Rebuilding internal_users.yml
- Reapplying security config with securityadmin.sh
- Diagnosing certificate DN mismatches in opensearch.yml
- After two days of troubleshooting, I rolled back to a clean snapshot and reinstalled using the official quickstart script
---
📸 Snapshot Taken
- Name: Wazuh Installed - Dashboard Functional
- Purpose: Baseline for future agent deployment and rule tuning

✅ Next Steps
- Add agents (Ubuntu, Kali, Windows)
- Ingest logs (auth, syslog, web)
- Build custom detection rules
- Document alerts and rule tuning
- Explore Wazuh API and integrations
---
🧠 Lessons Learned
- **Snapshot discipline is critical**: Taking snapshots before and after major changes provides a safety net for experimentation and rollback. It saved hours of recovery time and enabled clean reinstallation without residual config issues.
- **Wazuh’s security configuration is sensitive to YAML formatting**: Indentation, spacing, and structure in files like `internal_users.yml` and `opensearch.yml` must be precise. Even minor formatting errors can silently break authentication or dashboard access.
- **Certificate DN mismatches can block security updates**: The Distinguished Name (DN) in your TLS certificate must match the expected value in Wazuh’s OpenSearch config. If mismatched, `securityadmin.sh` will fail without clear error messaging.
- **Manual recovery builds real-world SOC troubleshooting skills**: Rebuilding missing config files, diagnosing silent failures, and validating service health under pressure mirrors real incident response scenarios.
- **Clean reinstall is sometimes the fastest fix**: After extensive troubleshooting, reverting to a clean snapshot and reinstalling Wazuh using the official script restored functionality faster than patching broken components.
- **Documentation is part of the solution**: Capturing each step, error, and fix not only helps future troubleshooting but also builds a strong portfolio artifact for SOC analyst roles.

---




