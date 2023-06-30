# Ansible role: Install Appimaged

[![License][license-image]][license-url] [![Ansible Galaxy][ansible-galaxy-image]][ansible-galaxy-url] [![Ansible Galaxy Quality][ansible-galaxy-quality-image]][ansible-galaxy-url] [![Ansible Galaxy Release][ansible-galaxy-release-image]][ansible-galaxy-url]

Install [Appimaged](https://docs.appimage.org/introduction/software-overview.html#appimaged) 4 any Linux

## Work on

### Ansible Galaxy style

```yaml
  platforms:
    - name: Fedora
      versions:
        - 35
    - name: Ubuntu
      versions:
        - jammy
        - bionic
        - focal
    - name: Debian
      version:
        - buster
        - bullseye
        - stable
        - oldstable
    - name: EL
      versions:
        - 8
    - name: opensuse
      vesrion:
        - 15.3
        - tumbleweed
```

## Requirements

min_ansible_version: 2.9

## Role Variables

```yaml
---
# https://unix.stackexchange.com/a/4187
appimaged_full_path_to_install: /usr/local/bin/appimaged-latest-x86_64.AppImage

# Create /etc/xdg/autostart/appimaged.desktop
appimaged_autostart: true

# ln -s $HOME/.local/share/applications/appimagekit_*.desktop "$XDG_DESKTOP_DIR"/
appimaged_create_symlinks_to_desktop: true

# Help Options. appimaged --help
appimaged_opt: -q

# If the key is not defined, the latest version will be downloaded from github (https://github.com/probonopd/go-appimage)
# appimaged_full_uri_path: rsync://10.10.10.10/soft/appimaged/appimaged-latest-x86_64.AppImage
# appimaged_full_uri_path: http://10.10.10.10/soft/appimaged/appimaged-latest-x86_64.AppImage
```

## HowTo

### How to install role

Over `ansible-galaxy`:

```bash
ansible-galaxy install don_rumata.ansible_role_install_appimaged
```

Over `bash+git`:

```bash
mkdir -p "$HOME/.ansible/roles"
cd "$HOME/.ansible/roles"
git clone https://github.com/don-rumata/ansible-role-install-appimaged don_rumata.ansible_role_install_appimaged
```

## Example Playbooks

### I

Install Appimaged for any supported plaforms, with autostart and symlinks:

`install-appimaged.yml`:

```yaml
- name: Install Appimaged
  hosts: all
  strategy: free
  serial:
    - "100%"
  roles:
    - don_rumata.ansible_role_install_appimaged
  tasks:
```

### II

Install Appimaged from **local** rsync server, without autostart and symlinks:

`install-appimaged.yml`:

```yaml
  - name: Install Appimaged
    hosts: all
    strategy: free
    serial:
      - "100%"
    roles:
      - role: don_rumata.ansible_role_install_appimaged
        appimaged_full_uri_path: rsync://10.10.10.10/soft/appimaged/appimaged-latest-x86_64.AppImage
        appimaged_autostart: false
        appimaged_create_symlinks_to_desktop: false
    tasks:
```

## License

Apache License, Version 2.0

## Author Information

[don Rumata](https://github.com/don-rumata)

## TODO

- Add tests.
- Add the ability to install appimagetool and mkappimage.

[license-image]: https://img.shields.io/github/license/don-rumata/ansible-role-install-appimaged.svg
[license-url]: https://opensource.org/licenses/Apache-2.0

[ansible-galaxy-image]: https://img.shields.io/badge/ansible_galaxy-don__rumata.ansible__role__install__appimaged-blue.svg
[ansible-galaxy-url]: https://galaxy.ansible.com/don_rumata/ansible_role_install_appimaged

[ansible-galaxy-quality-image]: https://img.shields.io/ansible/quality/56147

[ansible-galaxy-release-image]: https://img.shields.io/github/v/release/don-rumata/ansible-role-install-appimaged.svg?include_prereleases
