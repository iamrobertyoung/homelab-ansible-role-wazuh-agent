# homelab-ansible-role-wazuh-agent

[![Lint](https://github.com/iamrobertyoung/homelab-ansible-role-wazuh-agent/actions/workflows/lint.yml/badge.svg)](https://github.com/iamrobertyoung/homelab-ansible-role-wazuh-agent/actions/workflows/lint.yml)
[![Release](https://github.com/iamrobertyoung/homelab-ansible-role-wazuh-agent/actions/workflows/release.yml/badge.svg)](https://github.com/iamrobertyoung/homelab-ansible-role-wazuh-agent/actions/workflows/release.yml)
[![SLSA 3](https://slsa.dev/images/gh-badge-level3.svg)](https://slsa.dev)
[![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/iamrobertyoung/homelab-ansible-role-wazuh-agent/badge)](https://scorecard.dev/viewer/?uri=github.com/iamrobertyoung/homelab-ansible-role-wazuh-agent)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Ansible role for installing and configuring the Wazuh agent on Debian/Ubuntu systems.

## Requirements

- Ansible >= 2.15
- Target: Ubuntu (focal, jammy, noble) or Debian (bullseye, bookworm)

## Role Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `wazuh_manager_address` | `wazuh.local.iamrobertyoung.co.uk` | Wazuh manager address |
| `wazuh_manager_port` | `1514` | Wazuh manager port |
| `wazuh_agent_group` | `homelab` | Agent group for centralized configuration |
| `wazuh_agent_name` | `{{ inventory_hostname }}` | Agent name to register with manager |
| `wazuh_registration_password` | `""` | Registration password (if manager requires it) |
| `wazuh_repo_key_url` | `https://packages.wazuh.com/key/GPG-KEY-WAZUH` | Wazuh GPG key URL |
| `wazuh_repo_url` | `https://packages.wazuh.com/4.x/apt/` | Wazuh APT repository URL |

## Usage

### Install via requirements.yml

```yaml
- src: git@github.com:iamrobertyoung/homelab-ansible-role-wazuh-agent.git
  scm: git
  version: main
  name: wazuh_agent
```

```bash
ansible-galaxy install -r requirements.yml
```

### Example Playbook

```yaml
- hosts: servers
  become: true
  roles:
    - role: wazuh_agent
```

### Override defaults

```yaml
- hosts: servers
  become: true
  roles:
    - role: wazuh_agent
      vars:
        wazuh_manager_address: wazuh.example.com
        wazuh_agent_group: production
```

## What Gets Installed

- Wazuh APT repository and GPG key
- Wazuh agent package
- Agent configuration (`/var/ossec/etc/ossec.conf`)
- Agent service enabled and started

## Supply Chain Security

This project implements [SLSA](https://slsa.dev/) Level 3 provenance for release artifacts.

- Provenance attestations are submitted to [GitHub Attestations](https://github.com/iamrobertyoung/homelab-ansible-role-wazuh-agent/attestations)
- Release artifacts include `.intoto.jsonl` provenance files
- Security posture tracked via [OpenSSF Scorecard](https://scorecard.dev/viewer/?uri=github.com/iamrobertyoung/homelab-ansible-role-wazuh-agent)

### Verifying Release Provenance

```bash
# Using GitHub CLI (recommended)
gh attestation verify wazuh_agent-<VERSION>.tar.gz \
  --repo iamrobertyoung/homelab-ansible-role-wazuh-agent

# Or using slsa-verifier
VERSION="v1.2.0"  # Replace with desired version
slsa-verifier verify-artifact wazuh_agent-${VERSION}.tar.gz \
  --provenance-path wazuh_agent-${VERSION}.tar.gz.intoto.jsonl \
  --source-uri github.com/iamrobertyoung/homelab-ansible-role-wazuh-agent \
  --source-tag "${VERSION}"
```

## License

MIT
