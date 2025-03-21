# Project 1: Create VM using labs

## Overview
This project focuses on creating a VM in a lab environment. Lab was completed on https://portal.netdevgroup.com/

## Objectives
- Create a Virtual Machine
- Virtual Machine Files and Snapshots
- Virtual Machine Cloning and Exporting
- Virtual Machine Networking

## Questions leading to vSphere Projects 2,3,4 etc.
1. **Step 1**: How is NAT Setup on my organisations vSphere environment?
2. **Step 2**: 	- Printer?
		- Display graphics memory?
		- Select New CD/DVD (SATA) as the next device.
			* common storage protocol. SATA (Serial Advanced Technology Attachment) for Small-sized tower server, DAS.
		- Automatically power on VM after creation?
		- USB controller capability 2.0?

## Lubuntu vs Ubuntu

- **Lubuntu**:
  - Requires fewer system resources, making it ideal for older hardware.
  - Has a basic and straightforward interface.

- **Ubuntu**:
  - Has higher system requirements and is better suited for modern hardware.
  - Offers a more modern and polished user interface.

##Learnings
## Disk

1. **Specify Disk Capacity**:
   - Split virtual disk into multiple files to make it easier to move the VM to another computer.
   - The VM disk is stored as files on the host computer's physical disk.
   - Press `Win + X` on your keyboard and select "Disk Management".
   - Run a command to create a VMDK file that points to the physical disk.
	VMDK files are essential for creating and managing virtual machines in VMware environments. They store the VM's operating system, applications, and data, making it easy to manage and migrate VMs

## CPU

1. **Select VM Processors**:
   - Open the Task Manager.
   - Click on the "Performance" tab.
   - Select "CPU".

## Network Adapter (LAN)

1. **NAT**:
   - Used to share the host's IP address on a VM.
   - NAT (Network Address Translation) on virtual machines (VMs) is typically used when VMs need to access external networks, such as the internet, while keeping them isolated from the host machine's network.

2. **Bridged Networking**:
   - The VM gets its own IP address from the network's DHCP server.
   - It is connected directly to the physical network.

3. **Host-Only Networking**:
   - The VM can only communicate with the host machine and other VMs configured to use the same host-only network.
   - The VM does not have access to external networks like the internet.

4. **Internal Networking**:
   - The VM can only communicate with other VMs on the same internal network.
   - It is completely isolated from the host machine and any external networks.

