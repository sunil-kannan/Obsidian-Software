---
date: 2025-01-03
tags: 
link:
---

# Virtualization

> Virtualization is **technology that you can use to create virtual representations of servers, storage, networks, and other physical machines**.

## Hypervisor

A hypervisor, also known as a virtual machine monitor or VMM, is **software that creates and runs virtual machines (VMs)**. A hypervisor allows one host computer to support multiple guest VMs by virtually sharing its resources, such as memory and processing.

## Types of Hypervisor

### Type 1 Hypervisor (Bare-metal)

A hypervisor that runs directly on the physical hardware without needing an underlying operating system.
#### **Key Characteristics**:

1. **Direct Hardware Access**: Since it operates directly on the hardware, it has minimal latency and high performance.
2. **Independent**: Does not rely on a host operating system, reducing the attack surface and overhead.
3. **Use Cases**: Large-scale virtualization, enterprise-level server management, and cloud computing.
4. **Examples**:
    - VMware ESXi
    - Microsoft Hyper-V
    - Xen
    - Oracle VM Server for x86

### Hypervisor (Hosted)

A hypervisor that runs on top of a host operating system and uses the OS to interact with the hardware.
#### **Key Characteristics**:

1. **Dependent on Host OS**: The hypervisor relies on the host operating system for device drivers and hardware communication.
2. **Ease of Use**: Easier to install and manage, as it integrates with the existing operating system.
3. **Use Cases**: Development, testing, and running secondary operating systems on personal devices.
4. **Examples**:
    - VMware Workstation
    - Oracle VirtualBox
    - Parallels Desktop (macOS)
    - QEMU