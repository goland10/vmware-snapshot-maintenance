# vmware-snapshot-maintenance
Delete snapshots through the vCenter with Ansible

VMware Snapshot Management Automation
A streamlined Ansible utility for reporting and cleaning up aged VMware snapshots across multiple datacenters.
🚀 Overview
This automation helps maintain storage health by identifying and removing snapshots older than a specified threshold. It uses govc for sizing and the vmware_guest_snapshot module for lifecycle management.
Key Features
Aged Snapshot Cleanup: Deletes snapshots exceeding a defined number of days.
Automated Reporting: Generates CSV reports of existing snapshots and deletion logs.
Dynamic Inventory: Automatically builds inventory from templates per datacenter.
Safety First: Includes a tmux session check to prevent accidental job termination.
🛠 Prerequisites
Ansible Core: v2.15.8+
Govc CLI: vmware/govmomi (Required for snapshot sizing).
Credentials: LDAP user SnapshotBot@amdocs.com.
Clean Sessions: If govc hangs, remove ~/.govmomi/.
📖 Usage Examples
📊 Generating Reports
List snapshots older than 15 days for all DCs in your list:
bash
for DC in $(<DCs.txt); do 
  ansible-playbook -t report -e "day=15 dc=$DC" snapshot.yml
done
Use code with caution.

🧹 Removing Snapshots
Delete snapshots older than 60 days for GSS vCenter:
bash
for DC in $(<DCs.txt); do 
  ansible-playbook -t rm -e "day=60 dc=$DC" snapshot.yml
done
Use code with caution.

🎯 Targeted Action
Run cleanup for a specific datacenter and specific age:
bash
ansible-playbook -t rm -e "day=180 dc=ILRNA_BSS_DC" snapshot.yml
Use code with caution.

📝 Tags
pre: Initialize dynamic inventory.
report: Generate CSV reports of current snapshots.
rm: Perform snapshot deletion and log results.
