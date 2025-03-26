# Project 2: vSphere NAT and VLAN Configuration

## Questions

# NAT Setup of my organisation vSphere

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