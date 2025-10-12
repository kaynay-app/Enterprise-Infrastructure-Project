Built lightweight Kali Linux vm (KLM-MONITOR01) to monitor ping, and host-down/up status for the virtual environment (ESXi hosts, vCenter, DCs, Gateway, Workstations) with the following specs:
  - OS: Kali GNU/Linux Rolling
  - Memory: 2GB
  - CPU Core(s): 1
  - Hard Disk(SCSI): 30GB

**MONITORING TOOLS AND SETUP**

  - Tool: Uptime Kuma
  - Alert Instance: ICMP ping
  - Escalations: Email listed contact on file via gmail smtp relay messages

**Docker and Uptime Kuma Setup and Install**
First, we will install Uptime Kuma systems monitoring tool via docker. This keeps the servuce up to date and makes the startup automatic on boot. To install docker, run the following commands:

sudo apt update
sudo apt install docker.io -y
sudo systemctl enable --now docker

- To run Uptime Kuma run these commands to initiliaze it:
sudo docker run -d --restart=always -p 3001:3001 --name uptime-kuma louislam/uptime-kuma

- Once the install is successful, open a web browser and goto the url of your kali linux vm at port 3001.ex:
http://<Kali_vm_IP>:3001

- Create a new management account and setup your monitoring dashboard for your instaces and alerting groups

**NOTE for Kali:**
- If you use Docker, you don’t need any extra dependencies.
- Make sure  port 3001 is allwed on your Kali VM’s firewall.
- You should be able to access the monitoring dashboard from any device in your LAN.

