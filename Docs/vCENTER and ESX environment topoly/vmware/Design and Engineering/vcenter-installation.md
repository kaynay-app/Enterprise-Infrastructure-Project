+-------------------------------------------------------------+
| 🧑‍💻 vCenter Server Installation (Manual GUI)               |
+-------------------------------------------------------------+

The vCenter Server Appliance (VCSA) was installed manually using
the VMware GUI installer. This approach allowed for a 
guided and visual deployment process ideal for lab or production 
use.

+--------------------------+
| 🛠️ Installation Steps       |
+--------------------------+

1. Mounted the VCSA ISO on local workstation.
2. Launched the GUI installer:
     - `installer.exe` (Windows)
3. Selected **"Install"** to begin Stage 1 – Appliance Deployment.
4. Configured:
     • Target ESXi host for deployment
     • VM name and root password
     • Deployment size and target datastore compatible with my lab and license
     • Networking (static IP, FQDN, gateway, DNS, vMotion)
5. Continued to Stage 2 – Appliance Setup:
     • Time sync configuration (NTP/host)
     • SSO domain setup (`vsphere.local`)
     • Enabled SSH temporarily for system configuration 

+----------------+
| ✅ Result      |
+----------------+

• vCenter deployed and powered on successfully 
- Connected to primary ESXi host on KLM-VCL01 cluster
• Joined to the on-prem Active Directory domain  
• Web interface accessible via:  
  `https://klmvcenter01:443/ui`  
• Connected ESXi hosts and validated VM inventory  
• Ready for VM migration, monitoring, and automation tasks  


