# vmware-snapshot-maintenance
Delete snapshots through the vCenter with Ansible
# VMware Snapshot Management Automation

A streamlined Ansible utility for reporting and cleaning up aged VMware snapshots across multiple datacenters using the [community.vmware collection](https://docs.ansible.com).

## 🚀 Overview
This automation maintains VMs storage health by identifying and removing snapshots older than a specified threshold. It leverages `govc` for precise sizing and generates CSV reports for auditing.

### Key Features
*   **Aged Cleanup:** Deletes snapshots exceeding a defined `day` threshold.
*   **Automated Reporting:** Generates CSVs of existing snapshots and deletion logs.
*   **Dynamic Inventory:** Builds inventory on-the-fly from templates (`dc.vmware.j2`).
*   **Safety Check:** Requires an active `tmux` session to prevent job interruption.

## 🛠 Prerequisites
*   **Ansible Core:** [v2.15.8+](https://docs.ansible.com)
*   **Govc CLI:** Must be installed and in `$PATH`.
*   **Credentials:** LDAP user `SnapshotBot@amdocs.com`.
*   **Session Management:** If `govc` session issues occur, clear the cache: `rm -rf ~/.govmomi/`.

## 📖 Usage Examples

### 📊 Reporting
Generate a CSV report of snapshots older than 15 days for all datacenters listed in `DCs.txt`:
```bash
for DC in $(<DCs.txt) ; do 
  ansible-playbook -t report -e "day=15 dc=$DC" snapshot.yml 
done
