# Ansible Role: LinuxGSM

|Quality|Downloads|Version|
|-------|---------|-------|

[![Ansible Galaxy](https://img.shields.io/badge/galaxy-nginxinc.nginx-5bbdbf.svg)](https://galaxy.ansible.com/nginxinc/nginx)
[![License](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)


|[![quality](https://img.shields.io/ansible/quality/54616)](https://galaxy.ansible.com/obihoernchen/ansible-lgsm)|[![downloads](https://img.shields.io/ansible/role/d/54616)](https://galaxy.ansible.com/obihoernchen/ansible-lgsm)|[![Version](https://img.shields.io/github/release/obihoernchen/ansible-lgsm.svg)](https://github.com/obihoernchen/ansible-lgsm/releases/)|

Ansible role for [Linux Game Server Mangers](https://linuxgsm.com) install.  
Defaults to installing CS:GO.

Tested with Red Hat OS family.

## Example Playbook

```yaml
---
- name: Setup CS:GO Server
  hosts: all
  become: yes

  roles:
    - obihoernchen.lgsm
```

## Role Variables

These variables are set in `defaults/main.yml`:
```yaml
---
# Red Hat OS family only
lgsm_required_packages:
  - epel-release
  - curl
  - wget
  - tar
  - bzip2
  - gzip
  - unzip
  - util-linux
  - file
  - python3
  - binutils
  - bc
  - jq
  - tmux
  - glibc.i686
  - libstdc++
  - libstdc++.i686
  - nmap-ncat
lgsm_user: lgsm_admin
lgsm_group: lgsm_admin
lgsm_additional_groups: ""
lgsm_comment: Linux Game Server Manager
lgsm_installdir: /opt/lgsm
lgsm_installer_url: https://linuxgsm.sh
lgsm_installer_name: linuxgsm.sh
lgsm_install_server: false
lgsm_server: csgoserver
lgsm_server_config: "{{ lgsm_installdir }}/lgsm/config-lgsm/{{ lgsm_server }}/{{ lgsm_server }}.cfg"
lgsm_install_crons: true

# LGSM configs use a simple key="value" format to build the specific gameserver config
# For available options see the _default.cfg file of your server: https://github.com/GameServerManagers/LinuxGSM/tree/master/lgsm/config-default/config-lgsm
# Some csgoserver defaults
lgsm_server_config_content:
  ## Game Server Login Token (GSLT): Required
  # GSLT is required for running a public server.
  # More info: https://docs.linuxgsm.com/steamcmd/gslt
  gslt: ""

  ## Predefined Parameters | https://docs.linuxgsm.com/configuration/start-parameters
  # https://docs.linuxgsm.com/game-servers/counter-strike-global-offensive
  # [Game Modes]         gametype  gamemode  mapgroup (you can mix these across all Game Modes except Danger Zone, but use only one)
  # Arms Race            1         0         mg_armsrace
  # Classic Casual       0         0         mg_casualsigma, mg_casualdelta
  # Classic Competitive  0         1         mg_active, mg_reserves, mg_hostage, mg_de_dust2
  # Custom               3         0
  # Deathmatch           1         2         mg_deathmatch
  # Demolition           1         1         mg_demolition
  # Wingman              0         2
  # Danger Zone          6         0         mg_dz_blacksite (map: dz_blacksite), mg_dz_sirocco (map: dz_sirocco)
  gametype: "0"
  gamemode: "1"
  mapgroup: "mg_active"
  ip: "0.0.0.0"
  port: "27015"
  clientport: "27005"
  sourcetvport: "27020"
  defaultmap: "de_mirage"
  maxplayers: "16"
  tickrate: "64"

  ## Updating | https://docs.linuxgsm.com/commands/update
  updateonstart: "on"
```

## Requirements

None

## License

MIT

## Author Information

- Original role by [djroot2](https://github.com/djroot2)
- Improvements by [Obihoernchen](https://github.com/Obihoernchen)
