### Storage Management in Red Hat (RHEL)
Managing storage in Red Hat Enterprise Linux (RHEL) involves configuring, monitoring, and optimizing storage devices like hard drives, SSDs, and network storage. In Red Hat (RHEL) or any Linux-based system, storage can come in several forms. Here’s an overview of the main types of storage you can add to your system:
- Local Storage (HDD, SSD)
- Network File Systems (NFS)
- Storage Area Network (SAN)
- Server Message Block (SMB)/Common Internet File System (CIFS) - Samba
- Cloud Storage (AWS EBS, GCP Persistent Disk)

| Feature                      | **MBR (Master Boot Record)**                                       | **GPT (GUID Partition Table)**                                         |
| ---------------------------- | ------------------------------------------------------------------ | ---------------------------------------------------------------------- |
| **Partition Limit**          | Supports up to 4 primary partitions or 3 primary + 1 extended      | Supports up to 128 partitions without extended partitions              |
| **Disk Size Limit**          | Max size of 2TB                                                    | Can support disks larger than 2TB                                      |
| **Partition Type**           | Primary and Extended partitions                                    | Primary partitions only (with no need for extended partitions)         |
| **Boot Mode**                | Used with BIOS-based systems                                       | Used with UEFI-based systems                                           |
| **Data Structure**           | Stores partition table in the first sector of the disk (512 bytes) | Stores partition data in multiple places across the disk               |
| **Redundancy**               | No redundancy for partition table (single copy)                    | Redundant partition tables stored at the beginning and end of the disk |
| **Error Recovery**           | Lacks error checking or recovery mechanisms                        | Includes CRC32 checksums to improve data integrity and recovery        |
| **Compatibility**            | Compatible with older systems and most OSes                        | Supported by modern OSes and UEFI firmware                             |
| **Boot Partition**           | Bootloader must reside in the first 512 bytes of the disk          | No such constraint, bootloader can reside anywhere on the disk         |
| **Support for EFI**          | Does not support UEFI firmware boot                                | Required for UEFI boot systems                                         |
| **Partitioning Flexibility** | Limited flexibility, hard to change partitions after creation      | More flexible with partition sizes and modifications                   |
| **Usage**                    | Older systems and smaller disks (typically <2TB)                   | Modern systems, large disks (typically >2TB)                           |


**Local Storage (HDD, SSD):** Local storage in Linux, including Red Hat Enterprise Linux (RHEL), refers to physical disks and their partitions, logical volumes (if using LVM), and file systems that reside within the system. Below are the detailed steps and concepts for managing local storage, including checking storage type, partitioning, formatting, and building file systems.

Checking all available block devices
```bash
lsblk
```
Checking all available block devices in details
```bash
lsblk -l
```

