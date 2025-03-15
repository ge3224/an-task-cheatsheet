# Cheatsheets Task Module

This Ansible task module handles the installation and configuration of the
[cheat](https://github.com/cheat/cheat) command-line cheatsheet manager.

## Overview

This module:

- Creates necessary directories for cheat configuration
- Clones the community cheatsheets repository
- Sets up configuration files
- Creates symbolic links to custom cheatsheets

## Requirements

- Ansible 2.9+
- Git installed on the target machine
- `cheat` command-line tool already installed

## Variables

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `config_path` | Path to the cheat configuration file | Yes | - |
| `dest_path` | Base directory for installation (usually `/home/username`) | Yes | - |
| `cheatsheets_personal_path` | Path to personal cheatsheets repository | Yes | - |

## Usage

Example inclusion in a playbook:

```yaml
- name: Setup cheat configuration
  include_tasks: modules/cheatsheets/tasks/main.yml
  vars:
    config_path: "{{ playbook_dir }}/dotfiles/cheat/conf.yml"
    dest_path: "/home/johndoe"
    cheatsheets_personal_path: "{{ playbook_dir }}/dotfiles/cheat/personal"
```

An example playbook is provided in the `examples/` directory:

```bash
ansible-playbook examples/playbook.yml
```

## Notes

- All paths are validated before use
- Existing files are backed up or removed depending on their type
- The module is idempotent and will only perform actions when necessary
