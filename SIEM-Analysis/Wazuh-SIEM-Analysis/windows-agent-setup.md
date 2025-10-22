# 🪟 Windows Agent Setup (Wazuh 4.13)

**Author:** Festus Olise  
**Environment:** Windows 10 VM (VirtualBox), Wazuh Manager on Ubuntu

---

## 🧩 Overview

This guide documents the installation and configuration of the Wazuh agent on a Windows 10 virtual machine using the graphical interface. The agent connects to a Wazuh Manager running on Ubuntu and is monitored via the Wazuh Dashboard.

---

## 🛠️ Environment Details

- **VM Name:** `Windows_SOC`
- **OS:** Windows 10 Pro (x64)
- **Virtualization:** VirtualBox
- **Network:** Host-Only
- **Wazuh Manager IP:** `192.168.56.102`

---

## 📦 Agent Installation

### 1. Download the Installer

- Visit the official Wazuh agent download page:  
  [https://documentation.wazuh.com/current/installation-guide/installing-wazuh-agent/win.html](https://documentation.wazuh.com/current/installation-guide/installing-wazuh-agent/win.html)

- Download the latest `.msi` installer for Windows (Wazuh 4.13)

---

### 2. Run the Installer

- Double-click the `.msi` file
- Follow the installation wizard
- Accept the license agreement
- Choose default installation path

---

## 🔧 Agent Configuration (GUI)

### 1. Launch Wazuh Agent Manager

- Open **Wazuh Agent Manager** from the Start Menu

### 2. Configure Manager Connection

- Go to the **Configuration** tab
- Set the **Manager IP** to: `192.168.56.101` # This was the server IP in my home lab.
- Click **Save**

### 3. Start the Agent

- Go to the **Manage** tab
- Click **Start**
- Status should change to `Running`

---

## 📊 Dashboard Confirmation

- Go to **Wazuh Dashboard > Agents**
- Windows agent should appear as  **Active** in the Agents Summary Tab

---

## ✅ Next Steps

- Ingest Windows Event Logs (Security, System, Application)
- Simulate detection scenarios (e.g., failed logins, PowerShell abuse)
- Create custom rules and validate alerts
- Document findings in `alert-analysis.md`

---

