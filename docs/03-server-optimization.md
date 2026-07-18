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


# Server Optimization

# Objective

Optimize the Ubuntu Server installation to provide a lightweight, stable, and production-oriented environment for the Self-Healing Docker Monitoring Platform.

# Scope

This phase focuses on reducing unnecessary components, improving maintainability, preparing the operating system for Docker workloads, and establishing development best practices.

# Requirements

- Ubuntu Server 24.04 LTS
- Internet connectivity
- Sudo privileges
- Git installed

# Implementation

The following optimization tasks were completed:

- Updated the operating system packages.
- Removed unnecessary packages and services.
- Verified enabled system services.
- Preserved only essential networking and security services.
- Performed package cleanup using `apt autoremove`.
- Verified package dependencies before removal.
- Configured Git global settings.
- Enabled SSH commit signing.
- Verified signed commits.
- Configured Markdown Lint.
- Implemented Continuous Integration using GitHub Actions.
- Added Trivy security scanning workflow.
- Added Docker Compose validation workflow.
- Added Markdown validation workflow.
- Enabled Branch Protection rules.
- Created project documentation structure.

# Verification

The following verifications were successfully completed:

- System services reviewed.
- Required networking services remained active.
- SSH service operational.
- AppArmor enabled.
- UFW enabled.
- Git commit signing verified.
- GitHub displays commits as **Verified**.
- GitHub Actions completed successfully.
- Markdown validation passed.
- Trivy workflow executed successfully.

# Evidence

- Successful GitHub Actions executions.
- Verified commit signatures.
- Repository documentation.
- Optimization logs.

# Issues Encountered

- GitHub displayed commits as **Unverified**.
- Markdown validation failures.
- SSH signing key registered as an Authentication Key.

# Resolution

- Registered the SSH key as a GitHub Signing Key.
- Configured Git SSH signing.
- Fixed Markdown formatting issues.
- Added repository lint configuration.

# Result

A clean, lightweight, reproducible Ubuntu Server environment prepared for infrastructure deployment, containerized workloads, and security hardening.

# Next Steps

- Configure static IP.
- Configure UFW.
- Install Fail2ban.
- Harden SSH.
- Configure permanent remote administration using Termius.
