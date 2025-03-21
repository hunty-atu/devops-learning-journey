# Project 1: VMware vSphere Configuration Notes

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



## Questions

# NAT Setup on vSphere

## VLAN Port Groups
- In the Configure tab, expand the Settings section.
- Click on Port Groups.
- There are 30 VLAN port IDs.

## VLAN Types
- Example: Go to VMware HCIA Distributed Switch > Citrix_Hosts > ACTIONS > EDIT SETTINGS > VLAN Types (standard VLAN).
- Options:
  - **VLAN**: Standard VLAN configuration.
  - **VLAN Trunking**: Allows multiple VLANs on a single port.
  - **Private VLAN**: Provides isolation between ports within the same VLAN.

## Review VLAN Configurations
- Check the VLAN settings in your vSphere Client to understand how each VLAN is configured.

### Determine Network Type
- **NAT (Network Address Translation)**: Look for configurations where internal IP addresses are translated to external ones. This is typically set up in the network settings of your virtual machines or the router/firewall settings.
  - VMware HCIA Distributed Switch Netflow Collector IP address --, and Port Mirroring is no items found.
- **Bridged Networking**: Check if the VLAN is connected directly to the physical network interfaces. This allows VMs to communicate with external networks as if they were on the same physical network.
  - Network topology: Check the Uplinks to see how the physical network adapters are connected to the Distributed Switch.
- **Host-Only Networking**: Verify if the VLAN is isolated from external networks and only allows communication between VMs on the same host.
- **Internal Networking**: Ensure the VLAN is set up for communication between VMs on the same host without any external network access.

## Use Network Management Tools
- Tools like NetFlow, Port Mirroring, and Network Health Check can help you analyze and verify the network traffic and configurations.
- Enable Network Health Check on the Distributed Switch to verify VLAN configurations and ensure there are no misconfigurations.



	


- Printer?
- Display graphics memory?
- Select New CD/DVD (SATA) as the next device.
- Automatically power on VM after creation?
- USB controller capability 2.0?


##Tips
echo "Hello, World!" > file.txt
Double >>: Appends output to the end of a file, preserving the existing content.

echo "Hello, again!" >> file.txt