# ansible-containerd-nerdctl

Ansible role for installing and configuring [nerdctl](https://github.com/containerd/nerdctl) and [crictl](https://github.com/kubernetes-sigs/cri-tools) for [containerd](https://containerd.io/) on Linux hosts.

## Features

- Downloads and installs nerdctl (configurable version)
- Downloads and installs crictl (configurable version)
- Sets up rootless mode
- Installs prerequisites (e.g., `uidmap`)
- Creates a symbolic link from `nerdctl` to `docker`
- Cleans up temporary files

## Role Variables

Default variables are defined in `defaults/main.yaml`:

- `nerdctl_version`: Version of nerdctl to install (default: `2.1.3`)
- `nerdctl_url`: Download URL for nerdctl
- `crictl_version`: Version of crictl to install (default: `1.37.0`)
- `crictl_url`: Download URL for crictl
- `install_path`: Path to install binaries (default: `/usr/local/bin`)
- `temporary_folder`: Temporary working directory

## Directory Structure

```
ansible.cfg
main.yaml                # Example playbook
defaults/
  main.yaml              # Default variables
tasks/
  main.yaml              # Main task list
  0-setup_temporary_folder.yaml
  1-download_files.yaml
  2-extract_files.yaml
  3-copy_files.yaml
  4-post_install.yaml
  5-cleanup.yaml
meta/
  main.yaml              # Ansible Galaxy metadata
LICENSE
README.md
```

## Usage

Example playbook (`main.yaml`):

```yaml
- name: ContainerD NerdCTL Installation
  hosts: localhost
  become: true
  gather_facts: true
  vars:
    ansible_python_interpreter: /opt/ansible-venv/bin/python
  roles:
    - setup
```

## Requirements

- Ansible 2.9+
- Linux host
- Internet access to download nerdctl

## License

MIT

## Author

[rhattox-ansible](https://github.com/rhattox-ansible)
