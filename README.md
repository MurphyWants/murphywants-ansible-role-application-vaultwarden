# murphywants-ansible-role-application-vaultwarden

Purpose:

```
Image: 'vaultwarden/server' https://hub.docker.com/r/vaultwarden/server
tag: latest # unless otherwise specificed in the variables
```

This role will:

## Requirements/Dependencies
Uses the following modules:

Uses the following roles:

## Tags
Ansible role template with the following actions & tags:

Tag | Description
--- | ---
Setup/Baseline | Setup the application and apply the configuration baseline
Start | Start required services
Stop | Stop required services
Backup | Run the backup for the component or application or OS
Update | Update the component applications
Remove | Remove configurations and applications
Purge | Remove all configurations and applications relating to the app/component

## Variables
Variable | Default Value | Description
---|---|--- 
VAULTWARDEN_HTTP_PORT |  8082 | Host port for port mapping
VAULTWARDEN_PATH |  '/mnt/vaultwarden' | The location of the container persistent data. A parition will be created and mounted here if the folder doens't exist.
VAULTWARDEN_STORAGE_ZFS_POOL |  'apps_pool' | The Linux host's ZFS pool name, where the partiiton will be created from
VAULTWARDEN_STORAGE_ZFS_FS |  'vaultwarden' | The name of the filesystem that ZFS is creating
VAULTWARDEN_TIMEZONE |  "America/New_York" | 	Timezone of the container
VAULTWARDEN_PODMAN_SERVICE_ACCOUNT |  'srv_vaultwarden' | Unused, TODO implement this
VAULTWARDEN_CONTAINER_VERSION |  'latest' | Can be used to specify a specific version of the container to pull and use
VAULTWARDEN_FQDN |  'vaultwarden.domain.com' | Change this to your fully qualified domain name
VAULTWARDEN_SSL_CERT_PATH |  | Requried for nginx config
VAULTWARDEN_SSL_KEY_PATH |  | Requried for nginx config


## Example Playbook

playbook.yml
```
- hosts: all 
  gather_facts: yes
  become: yes
  roles:
  - role: murphywants-ansible-role-application-vaultwarden
```

## Example Inventory

static.ini
```
[all]
rhel-vaultwarden.domain.example.com

[app_vaultwarden]
rhel-vaultwarden.domain.example.com

[app_vaultwarden:vars]
VAULTWARDEN_URL="vaultwarden.domain.example.com"
```

# TODO List
- [ ] Implement further backups
  - [ ] ZFS snapshots
  - [ ] Borg Backup