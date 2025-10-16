# 🐙 Kali Linux Agent Setup (Wazuh 4.13)

**Author:** Festus Olise  
**Environment:** Kali Linux VM (VirtualBox), Wazuh Manager on Ubuntu

---

## 🧩 Overview

This guide documents the manual installation and configuration of the Wazuh agent on a Kali Linux VM. The agent connects to a Wazuh Manager running on Ubuntu and is visible in the Wazuh Dashboard.

---

## 🛠️ Environment Details

- **VM Name:** `Kali_SIEM`
- **OS:** Kali Linux (Rolling)
- **Virtualization:** VirtualBox
- **Network:** Bridged Adapter
- **Wazuh Manager IP:** `192.168.56.102`

---

## 📦 Agent Installation (Manual Method)

### 1. Add Wazuh GPG Key and Repository

```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --dearmor | sudo tee /usr/share/keyrings/wazuh.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
```
### 2. Update and Install Agent
```bash
sudo apt update
sudo apt install wazuh-agent
```
- 🔧 Agent Configuration
- 1. Set Manager IP
- Edit the agent config
```bash
sudo nano /var/ossec/etc/ossec.conf
```
- Update the <server> block:
```xml
<server>
  <address>192.168.56.102</address>
</server>
```
- 2. Start and Enable Agent
```bash
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```
- 3. Verify Agent Status
```bash
sudo systemctl status wazuh-agent
```
- 🧠 Notes
- No authentication key or password is required for default manager setups
- Agent version can be pinned to prevent auto-updates:
```bash
sudo apt-mark hold wazuh-agent
```
---
✅ Next Steps
- Ingest logs: /var/log/auth.log, /var/log/syslog, /var/log/apache2/access.log
- Create custom rules in local_rules.xml
- Simulate detection scenarios (e.g., failed SSH login)
- Document alerts and rule tuning
