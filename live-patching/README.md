# Live Patching

Live patching is reserved for high severity security related patches (think CosmicSting, SessionReaper), that need to be released to production ASAP. Where we will typically skip the usual deployment/testing process and patch the current deployments.

This is a process that can be done in as little as 5 minutes, if your brave enough. Or a few hours if you opt to perform a slower rolling release.

```sh
curl https://raw.githubusercontent.com/magento/magento-cloud-patches/xxxx.patch > patches/CVE-2025-54236.patch
ansible-playbook -i inventories/acme_agency.yaml playbooks/patch.yaml -e patch_file=patches/CVE-2025-54236.patch
```

> ℹ **Bonus Tip:** You can start with targeting a single/smaller selection of hosts with the `--limit` flag. Then once confident push across the whole inventory.

## Example Demo

You can create a demo environment by using Vagrant. This will deploy 3 containers, with a mock Magento application installed. 
You may need to adjust the IP Addresses for the containers within both the `demo/Vagrantfile` and `inventories/acme_agency.yaml` files.

```sh
# Test Applying a patch
ansible-playbook -i inventories/acme_agency.yaml playbooks/patch.yaml -e patch_file=patches/CVE-2025-54236.patch

# Test Revert a patch
ansible-playbook -i inventories/acme_agency.yaml playbooks/patch.yaml -e patch_file=patches/CVE-2025-54236.patch -e revert=1

# Test Applying a patch to a subset of the inventory
ansible-playbook -i inventories/acme_agency.yaml playbooks/patch.yaml -e patch_file=patches/CVE-2025-54236.patch --limit "client-01,client-02"
```