# kali multi-network adapters

If facing error while enabling multiple network adapter for Debian (VirtualBox or VMware):

## Fix

1. Right click Network Icon > Edit Connections
2. Remove all Ethernet connections
3. Add each Ethernet adapter manually, setting `Device` under `Ethernet` tab properly.
4. Save