- Host upgraded from ESXi 7.0.0	ESXi 7.0 GA	2020/04/02	15843807 to ESXi 7.0.3 EP13	ESXi 7.0 Update 3s	2025/03/04	24585291	Patch
  manually with .zip image depot file due to Lifecycle Manager update token links for eval licenses

- Downloaded Image depot from broadcom site and placed in a shared datastore accessible to all ESXi hosts with WinSCP and, SSH into individual hosts
- Placed hosts in maintenance mode, allow VMs migration to complete and, begin installing upgrade file 
