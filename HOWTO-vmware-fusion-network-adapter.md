# How to manually remove VMware Fusion Virtual Network Adapter

See also http://thornelabs.net/2013/10/18/manually-add-and-remove-vmware-fusion-virtual-adapters.html

```bash
cat /Library/Preferences/VMware\ Fusion/networking
sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cfgcli vnetcfgremove VNET_5_DHCP
sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cfgcli vnetcfgremove VNET_5_DHCP_CFG_HASH
sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cfgcli vnetcfgremove VNET_5_HOSTONLY_NETMASK
sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cfgcli vnetcfgremove VNET_5_HOSTONLY_SUBNET
sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cfgcli vnetcfgremove VNET_5_VIRTUAL_ADAPTER
```

Restart VMware Fusion networking
```bash
sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cli --configure
sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cli --stop
sudo /Applications/VMware\ Fusion.app/Contents/Library/vmnet-cli --start
ifconfig
```
