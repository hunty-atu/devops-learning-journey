Project3: Tasks and notes on various VM files and settings within a vSAN cluster.

vSphere Client version 7.0.3.01900.

VxRail-Virtual-SAN-Datastore store virtual machine files and other data within a vSAN cluster.
   **Test**:
   - Locate open the `VsP.vmx` file contents, observe the `memsize = “32768”` line. This is the VM’s current memory size.


1. **Investigate the Various Files**:
   - **VMDK**: Virtual Machine Disk file that stores the contents of the virtual machine's hard drive.
   - **VMX**: Virtual Machine Configuration file containing settings such as the virtual hardware configuration, network settings, and other parameters.
   - vshere: Virtual Machine Disk Descriptor file containing metadata about the virtual disk.
   - **VMXF**: Virtual Machine Team Configuration file used when virtual machines are part of a team.
   - **Log Files**: Record the activity of the virtual machine, useful for troubleshooting.
   - **Snapshot Files (VMSN and VMSD)**: VMSN stores the state of the virtual machine at the time the snapshot was taken, including the memory state. VMSD contains metadata about the snapshots.

2. ## Identify the VM Settings and Where They Are Stored

- **.dvsData**: Related to distributed virtual switches (DVS) and contains network configuration data.
- **.sdd.sf**: Part of the snapshot delta disk structure, used to manage snapshots.
- **.hlog**: Host log file containing logs related to the VM's operations on the host.
- **.nvram**: Stores the BIOS or EFI configuration of the VM.
- **.vmsd**: Contains metadata and information about the VM's snapshots.
- **.vmtx**: Template configuration file, indicating that the VM is a template rather than a regular VM.
- **.vmdk**: Virtual disk file containing the actual data of the VM. For example, `Windows 11 Template_6.vmdk` is the virtual disk for your Windows 11 template.

## Address download operation issues:

- **Permissions**: Ensure you have the necessary permissions to download files from the datastore.
- **File Locks**: If the VM is powered on, certain files like `.nvram` might be locked. Try powering off the VM before downloading.
- **Datastore Browser**: Use the vSphere Client directly connected to the ESXi host where the VM is running.

**NB: ESXi is designed to create and manage multiple virtual machines on a single physical server, while vSphere is an entire solution. Use the Command Mv to update file names.