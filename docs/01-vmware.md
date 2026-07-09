# VMware Virtual Machine

# Objective

Create a lightweight and reproducible virtual machine that will serve as the foundation for the Self-Healing Docker Monitor Platform.

# Scope

This phase covers the virtual machine creation and resource allocation before installing the operating system.

# Requirements

- VMware Workstation
- Ubuntu Server 24.04 LTS ISO
- 30 GB virtual disk
- 2 vCPU
- 4 GB RAM
- Bridged Network Adapter

# Implementation

The virtual machine was created using the following configuration:

- Hypervisor: VMware Workstation
- Guest OS: Ubuntu Server 24.04 LTS
- CPU: 2 vCPUs
- Memory: 4 GB
- Disk: 30 GB
- Network Mode: Bridged
- OpenSSH support planned during OS installation

The virtual machine was intentionally deployed without a graphical interface to minimize resource consumption.

# Verification

The VM booted successfully and detected the virtual hardware correctly.

# Evidence

Pending screenshots.

# Problems Found

None.

# Solution Applied

Not applicable.

# Result

A clean virtual machine was successfully prepared for Ubuntu Server installation.

# Next Steps

- Install Ubuntu Server
- Configure networking
- Optimize the operating system
