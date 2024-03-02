# Proxmox Mesh Node Setup

A quick guide to getting aredn running as a virtual machine on the x86 hypervisor, Proxmox. 
This may be handy for hosting a tunnel capable of more users than a router. 
This guide is a **work in progress**, and makes the assumption that your proxmox server is on your non-aredn internal network using one adapter.

## Preparations
Click the name of the host in your datacenter you will be putting your vm on
Expand the **System** section if needed and click **Networking**
Double click the **Linux bridge** device that your machine will use (Usually **vmbr0** by default on a machine with one network card)
Enable the **VLAN aware** checkbox and click **Ok**
Reboot your proxmox host

## Creation
Click **Create VM**
General tab: set a machine name
OS tab: select **Do not use any media** and leave the guest as **Linux** version **6.x - 2.6 Kernel**
System tab: leave defaults
Disks tab: click the trashcan icon next to scsi0
CPU tab: set Sockets to 1 and Cores to 2
Memory tab: set between 64mb (bare minimum) and 1024mb (max recommended)
Network tab: likely defaults, vmbr0, leave VLAN tag blank (aredn vm handles these internally)
Confirm tab: leave **Start after created** unchecked, take note the vmid for later, and click **Finish**

## Aredn installation
SSH to your proxmox host

Download the latest x86-64-generic-ext4-combined.img.gz with wget, at the time of writing:
```
wget http://downloads.arednmesh.org/releases/3/23/3.23.12.0/targets/x86/64/aredn-3.23.12.0-x86-64-generic-ext4-combined.img.gz
```
Extract the image:
```
gunzip aredn-3.23.12.0-x86-64-generic-ext4-combined.img.gz
```
Copy the image into your main storage (in my case, local-lvm) assigned to your vmid from earlier (in my case, 113)
```
qm disk import 113 aredn-3.23.12.0-x86-64-generic-ext4-combined.img local-lvm
```
Back in the web interface, open the hardware section of your aredn vm, double click the unassigned disk, and click **Add**
In the **Options** section, double click **Boot order** and place a check on scsi0 and click **Ok**

## Initial configuration
Start the VM and click **Console**
Once the VM has finished booting, press Enter to drop to a shell
Set the ip address to something in your lan's subnet, in my case:
```
ifconfig br-lan 192.168.15.80
```
In your browser, go to that address (http://192.168.15.80) and complete the initial node setup

## VLAN setup
Once the node has rebooted, you likely need to change the vlan tagging so the wan gets an address from your internet router and the aredn lan is tagged so it doesn't interfere with your home lan
From the proxmox Console, Edit /etc/config/network in the "Lan configuration" section change ":u" to ":t" and in the "WAN configuration" change ":t" to ":u", save, exit, then
```
service network restart
```
You can check the ip of br-wan by:
```
ip a
```
Browse to the aredn web setup and configure your static IP. Once it reboots, edit /etc/aredn_include/swconfig to reflect the Lan and Wan sections from /etc/config/network with the changes above, for example:
```
#### LAN configuration

config bridge-vlan
	option device 'br0'
	option vlan '3'
	list ports 'eth0:t'

config device
	option name 'br-lan'
	option type 'bridge'
	option macaddr 02:B2:D6:DB:22:96
	list ports 'br0.3'

config interface lan
	option device 'br-lan'
	option proto 'static'
	option ipaddr '10.59.71.249'
	option netmask '255.255.255.248'
	option dns '8.8.8.8 8.8.4.4'


#### WAN configuration

config bridge-vlan
	option device 'br0'
	option vlan '1'
	list ports 'eth0:u'

config device
	option name 'br-wan'
	option type 'bridge'
	option macaddr 02:20:C6:22:30:1E
	list ports 'br0.1'

config interface wan
	option device 'br-wan'
	option proto 'static'
	option ipaddr '192.168.15.80'
	option netmask '255.255.255.0'
	option gateway '192.168.15.1'
```
All set!(?)
