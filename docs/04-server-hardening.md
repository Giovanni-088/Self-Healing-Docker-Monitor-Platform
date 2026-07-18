# Server Hardening

# Objective

Document all security measures that will be implemented to secure the server before deploying production services.

# Scope

Operating system security, SSH hardening, firewall configuration and authentication improvements.

# Requirements

- Ubuntu Server
- OpenSSH
- Administrative privileges

# Implementation

Pending.

# Verification

Pending.

# Evidence

Pending screenshots.

# Problems Found

None.

# Solution Applied

Not applicable.

# Result

Pending implementation.

# Next Steps

- Configure SSH key authentication
- Disable password authentication
- Disable root login
- Configure UFW
- Install Fail2ban
- Configure permanent access from Termius
# Server Hardening

## Objective

Harden the Ubuntu Server 24.04 LTS virtual machine to provide a secure and stable foundation for the Self-Healing Docker Monitoring Platform.

The objective is to reduce the attack surface, enforce secure authentication, enable network protection, and prepare the server for production-like workloads.

---

## Scope

This phase includes:

- Static IP configuration
- SSH key authentication
- Password authentication disablement
- UFW firewall configuration
- Fail2ban deployment
- SSH daemon hardening
- Time synchronization verification
- Git SSH commit signing
- Security validation

---

## Requirements

- Ubuntu Server 24.04 LTS
- OpenSSH Server
- sudo privileges
- UFW
- Fail2ban
- Git
- SSH key pair
- Internet connectivity

---

## Implementation

### 1. Static IP Address

The server network configuration was migrated from DHCP to a static IPv4 configuration using Netplan.

Configuration included:

- Static IP
- Default gateway
- Cloudflare DNS
- Disabled DHCP

Example:

```yaml
network:
  version: 2
  ethernets:
    ens33:
      dhcp4: false
      dhcp6: false
      addresses:
        - 192.168.16.128/24
      routes:
        - to: default
          via: 192.168.16.2
      nameservers:
        addresses:
          - 1.1.1.1
          - 1.0.0.1
```

Configuration applied using:

```bash
sudo netplan apply
```

---

### 2. SSH Key Authentication

An ED25519 SSH key pair was created for secure authentication.

Authentication using public keys was successfully verified.

Passwordless login was tested locally before disabling password authentication.

Verification:

```bash
ssh -i ~/.ssh/id_ed25519 localhost
```

---

### 3. SSH Hardening

The SSH daemon configuration was updated with secure settings.

Implemented:

- Public key authentication enabled
- Password authentication disabled
- Root login disabled
- Empty passwords disabled
- X11 forwarding disabled
- TCP forwarding disabled
- Agent forwarding disabled
- Tunnel forwarding disabled
- Maximum authentication attempts reduced
- Login timeout reduced
- Client keepalive configured

Relevant directives:

```text
PubkeyAuthentication yes
PasswordAuthentication no
PermitRootLogin no
PermitEmptyPasswords no
X11Forwarding no
AllowTcpForwarding no
AllowAgentForwarding no
PermitTunnel no
MaxAuthTries 3
LoginGraceTime 30
ClientAliveInterval 300
ClientAliveCountMax 2
TCPKeepAlive no
```

Configuration validated using:

```bash
sudo sshd -t
```

---

### 4. UFW Firewall

The firewall was enabled with a default deny policy.

Configuration:

- Incoming traffic denied
- Outgoing traffic allowed
- SSH port allowed

Duplicate SSH rules were detected and removed.

Final configuration contains only the required SSH rule.

Verification:

```bash
sudo ufw status verbose
```

---

### 5. Fail2ban

Fail2ban was installed and configured to protect SSH against brute-force attacks.

Custom configuration:

```ini
[DEFAULT]
bantime = 1h
findtime = 10m
maxretry = 5
backend = systemd

[sshd]
enabled = true
```

Service enabled:

```bash
sudo systemctl enable fail2ban
sudo systemctl restart fail2ban
```

Verification:

```bash
sudo fail2ban-client status
sudo fail2ban-client status sshd
```

---

### 6. Time Configuration

The system timezone was changed from UTC to the local timezone.

Configured timezone:

```
America/Mexico_City
```

Verification:

```bash
timedatectl
```

NTP synchronization remained enabled.

---

### 7. Git SSH Commit Signing

SSH-based Git commit signing was configured.

Completed tasks:

- Signing key generated
- Git configured to use SSH signatures
- Allowed signers configured
- Signature verification completed successfully

Verification:

```bash
git log --show-signature -1
```

Result:

```
Good "git" signature
```

---

## Verification

The following components were successfully validated:

- Static IP address
- DNS resolution
- SSH public key authentication
- SSH daemon configuration
- UFW firewall
- Fail2ban service
- Time synchronization
- Git SSH commit signing

---

## Evidence

Verification commands:

```bash
hostnamectl

timedatectl

ip a

ip route

sudo ufw status verbose

sudo systemctl status ssh

sudo systemctl status fail2ban

sudo fail2ban-client status sshd

git log --show-signature -1
```

---

## Problems Encountered

### Duplicate SSH Firewall Rules

Issue:

Duplicate OpenSSH firewall rules were present.

Impact:

Redundant firewall configuration.

Resolution:

Removed duplicated rules using UFW numbered deletion.

---

### Fail2ban Configuration Conflict

Issue:

Fail2ban failed to start.

Error:

```
section 'sshd' already exists
```

Cause:

The entire default `jail.conf` had been copied into `jail.local`, resulting in multiple `[sshd]` definitions.

Resolution:

- Backed up the original configuration.
- Removed the oversized `jail.local`.
- Created a minimal override configuration containing only local settings.
- Restarted and validated the service.

---

### SSH Public Key Authentication

Issue:

SSH login initially requested a password.

Cause:

Public key authentication had not been fully verified before disabling password authentication.

Resolution:

- Verified the public key inside `authorized_keys`.
- Tested SSH authentication using the ED25519 key.
- Confirmed successful passwordless login.
- Disabled password authentication safely.

---

### Git Commit Signing Displayed "Unverified"

Issue:

Git locally reported a valid SSH signature while GitHub displayed the commit as **Unverified**.

Cause:

The SSH signing key had been uploaded as an Authentication Key instead of a Signing Key.

Resolution:

- Registered the key under **SSH Signing Keys**.
- Updated Git configuration.
- Regenerated the signed commit.
- Verified the signature locally and on GitHub.

Result:

```
Verified
```

---

## Result

The Ubuntu Server is now hardened and ready to host production-like Docker workloads.

Implemented security measures include:

- Static networking
- SSH key authentication
- Password login disabled
- Root login disabled
- Firewall protection
- Brute-force mitigation
- Secure SSH daemon configuration
- Time synchronization
- Verified Git SSH commit signing

---

## Next Steps

- Install Docker Engine
- Install Docker Compose
- Deploy Prometheus
- Deploy Grafana
- Deploy Node Exporter
- Deploy cAdvisor
- Deploy Alertmanager
- Configure Nginx Reverse Proxy
- Begin Watchdog development
