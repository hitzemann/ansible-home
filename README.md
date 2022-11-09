# Ansible Playbooks for my home network

## Prereqs

1. [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) should be installed on your control node, but nothing needs to be installed on your OpenWrt devices.

2. These playbooks depend on `gekmihesg.openwrt`. Install it using

    ```
    ansible-galaxy install gekmihesg.openwrt
    ```

3. These playbooks depend on `nn708.openwrt`. Install it using

    ```
    ansible-galaxy collection install nn708.openwrt
    ```

## Other TODOs

Change inventory.yaml to your needs. This is an example with a full featured OpenWRT Router, 2 dumb APs and a non OpenWRT machine.
It is important that all OpenWRT hosts are member of the openwrt group. Otherwise `gekmihesg.openwrt` will not run. `nn708.openwrt` depends on `gekmihesg.openwrt` so these roles won't work either if you do not put the hosts in the openwrt group.

Create `group_vars/openwrt` - preferably as a vault and add the following vars:
- `pppoe-user`: The username needed for your PPPoE uplink
- `pppoe-pass`: The password for `pppoe-user`
- `wifi-ssid`: Your SSID
- `wifi-pass`: The password for your SSID
- `zerotier-networkid`: The ID of the zerotier network to join
- `zerotier-secret`: The zerotier secret string. This is a bit tricky as it is generated after joining manually once.

The last two are not mandatory, I already test if they are defined otherwise the task is skipped.
