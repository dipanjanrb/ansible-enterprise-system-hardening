# Enterprise Linux Hardening & Configuration Management with Ansible

[![Ansible Lint](https://github.com/dipanjanrb/ansible-enterprise-system-hardening/actions/workflows/molecule.yml/badge.svg)](https://github.com/dipanjanrb/ansible-enterprise-system-hardening/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Ansible Core: >= 2.15](https://img.shields.io/badge/Ansible%20Core-%3E%3D%202.15-EE0000.svg)](https://docs.ansible.com/)
[![Target OS: RHEL / Ubuntu](https://img.shields.io/badge/Target%20OS-RHEL%20%2F%20Ubuntu-orange.svg)](https://access.redhat.com/)

Production-grade Ansible automation suite implementing **CIS (Center for Internet Security) Level 1 & Level 2 Server Hardening**, automated kernel parameter tuning, firewall management, and observability daemon deployment across hybrid multi-cloud infrastructure.

---

## 🛡️ Hardening Standards Implemented
* **SSH Hardening:** Enforce Protocol 2, disable `root` login, disable password authentication, restrict ciphers to modern curve algorithms (`ed25519`), enforce strict idle timeouts.
* **Kernel & Sysctl Hardening:** Disable IP forwarding, enable TCP SYN cookies, disable ICMP redirects, enable ASLR (Address Space Layout Randomization), protect against buffer overflows.
* **Firewall Enforcement:** Dynamic `firewalld` (RHEL/CentOS) and `ufw` (Ubuntu/Debian) lockdown with default-deny ingress policy.
* **Audit & Compliance:** Enforce `auditd` system call monitoring for unauthorized changes to `/etc/passwd`, `/etc/sudoers`, and system clock manipulations.
* **Observability Integration:** Automated deployment and systemd lifecycle management of Prometheus `node_exporter` with TLS and basic authentication.

---

## 📁 Repository Structure

```text
├── .github/
│   └── workflows/
│       └── molecule.yml              # CI: Ansible-lint and Molecule test matrix
├── inventory/
│   └── production/
│       ├── hosts.ini                 # Production host inventory
│       └── group_vars/
│           └── all.yml               # Global variable declarations
├── roles/
│   ├── cis_hardening/                # Core CIS benchmark OS hardening
│   │   ├── defaults/main.yml
│   │   └── tasks/
│   │       ├── main.yml
│   │       ├── ssh.yml
│   │       ├── sysctl.yml
│   │       └── firewall.yml
│   └── node_exporter/                # Prometheus metrics exporter
│       ├── tasks/main.yml
│       ├── handlers/main.yml
│       └── templates/node_exporter.service.j2
├── ansible.cfg                       # Optimized pipelining and SSH multiplexing
└── site.yml                          # Master playbook entrypoint
```

---

## 🚀 Usage

### 1. Requirements
* Ansible Core >= 2.15
* Python 3.10+
* OpenSSH with private key authentication configured

### 2. Run Playbook in Dry-Run / Check Mode
```bash
ansible-playbook -i inventory/production/hosts.ini site.yml --check --diff
```

### 3. Apply Hardening & Baseline Configuration
```bash
ansible-playbook -i inventory/production/hosts.ini site.yml
```

---

## 🧪 CI/CD & Testing
Every commit and Pull Request runs:
* `ansible-lint` to enforce code quality and anti-pattern prevention.
* `molecule test` using Docker containers across Ubuntu 22.04 and Rocky Linux 9.

---

## 📄 License
Licensed under the [MIT License](LICENSE).
