# Server Optimization

# Objective

Reduce resource consumption, remove unnecessary components and prepare the operating system for production-like workloads.

# Scope

System cleanup and performance optimization.

# Requirements

- Ubuntu Server 24.04 LTS
- Administrative privileges

# Implementation

The following tasks were completed:

- Removed Apport
- Removed Pollinate
- Removed PackageKit
- Removed Snap
- Removed LXD Installer
- Removed Open-iSCSI
- Removed Multipath Tools
- Removed Crash utilities
- Removed Kdump utilities
- Removed OS-Prober

System services were reviewed and unnecessary services were disabled.

System logging was optimized through journald configuration.

Kernel parameters were optimized using sysctl.

Open file limits were increased.

APT was configured to avoid installing recommended packages automatically.

# Verification

The following commands were executed:

systemctl list-unit-files --state=enabled

systemd-analyze

systemd-analyze blame

free -h

df -h

Package dependencies were also reviewed before removing orphan packages.

# Evidence

Pending screenshots.

# Problems Found

The autoremove simulation identified packages that could affect future project phases.

# Solution Applied

The automatic removal was postponed.

Only cache cleanup was performed until all project dependencies are installed.

# Result

The server is lighter, cleaner and prepared for security hardening.

# Next Steps

- Configure static networking
- Configure SSH
- Harden the operating system
