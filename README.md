# Enterprise-Infrastructure-Project
Cloud/On-premise enterprise virtual environment infrastructure project with High Availability features

# 🏗️ Private Cloud Infrastructure Lab (On-Prem /Cloud Virtual)

This project documents the **planning, build, and upgrade of a complete VMware-based on-premises virtual datacenter**, built using VMware Workstation as the foundation. It includes domain controllers, DNS, WSUS, iSCSI shared storage, domain-joined ESXi hosts and vCenter, and PowerShell-based VM alerting.

The lab simulates a **resilient private cloud environment** and is used to test system recovery, infrastructure upgrades, automated monitoring, and VM migrations.

---

## 📋 Contents

- 🗺️ Network & Infrastructure Topology
- 🖥️ ESXi Host Deployment & Upgrade Process
- 🧠 vCenter Recovery & Cold Migration Strategy
- 🖧 Shared Storage Setup (iSCSI via Windows Server)
- 🧱 Active Directory + DNS + WSUS Architecture
- 🔄 Live & Cold VM Migration Testing (vMotion)
- 💬 PowerShell-based Alerting via SMTP
- ⚠️ Troubleshooting Logs
- 📚 Lessons Learned & Next Steps

---

## 🧰 Technologies Used

- VMware ESXi 7.0U3s (nested in VMware Workstation)
- vCenter Server Appliance (VCSA)
- Windows Server 2016/ 2019 / 2022/ 2025
- Win10_22H2_English_x64
- Win11_24H2_English_x64
- Kali Linux
- Kuma Uptime
- SMTP Messaging Alerting
- Nmap - Zenmap GUI
- Active Directory Domain Services (ADDS)
- DNS, WSUS (KLM-DC02), iSCSI Target (KLM-DC01)
- iSCSI Shared Storage (MS iSCSI Target on Server)
- PowerShell (monitoring & alerting scripts)
- SMTP (email alerting for VM outages)
- VMware Workstation Pro
- VMware-VMvisor-Installer-7.0.x
- VMware-VCSA-all-7.0.x
- GitHub (project documentation)

---

## 🧠 Active Directory & Domain Services

- `KLM-DC01`: Primary domain controller  
  - Provides **iSCSI shared storage** via MS iSCSI Target  
  - Hosts **DNS** services  

- `KLM-DC02`: Secondary DC  
  - Runs **Windows Server Update Services (WSUS)**  
  - DNS server for fault tolerance  

- `KLM-DC03`: Tertiary DC  
  - Provides **additional DNS & AD** services  

All components are part of the domain `klm.king.klm`.

---

## 📦 vCenter & ESXi

- vCenter (KLMVCENTER01) and all ESXi hosts are **domain joined**
- Hosts were **upgraded** to ESXi 7.0U3s after deployment with manual .zip file upgrade 
- **Cold migration** used as fallback when vMotion failed
- vMotion issues resolved by aligning **network policies** across vSwitches

---

## 🛎️ Monitoring & Alerting

- Custom **PowerShell scripts** monitor VM power states
- If a VM is **down or unresponsive**, a script triggers:
  - An alert via **SMTP email**
  - Optional log output or escalation steps

---

## 🔄 VM Migration Example

VMs (including vCenter) were tested for:
- Live migration (vMotion) between upgraded hosts
- Cold migration fallback when vMotion failed
- Networking compatibility issues across ESXi hosts
- DNS resolution post-migration

---

## 🛠 Troubleshooting Highlights

- Resolved low memory issues (`stagebootbank` ramdisk)
- Addressed failed `lwsmd` process after upgrade
- Manually powered off VMs from CLI when unresponsive
- Re-registered VMs using `vim-cmd` after migration failures
- Updated CPU core settings to bypass ESXi hardware warnings in nested lab
- Performed upgrades with Image Depot baselines and manual .zip upgrades

---

## 📝 Status

✅ Fully functional & documented  
- Enabled vSphere HA and DRS
- Integrated syslog and centralized logging  
- Deployed Linux and Windows workload VMs

---

## 💡 Why This Project?

-To simulate a **production-grade private cloud lab**, replicating enterprise-level systems for:
- Disaster recovery testing with backups and snapshots 
- Infrastructure automation  
- Host patching and upgrade paths  
- AD-integrated VMware infrastructure  
- Hands-on experience with core IT systems
