# Plex Pipeline

Deploy plex as a Docker container at home (or wherever)


## Requirements

- Ubuntu Linux Host
- 8GB+ RAM

## Setting Up

### Add a Role

Add a `group_vars` folder which will include `vars.yml` (for group variables) and `vault.yml` (for Ansible vault).


Required variables for the playbook are:

```
# vars.yml
install_version
time_zone


# vault.yml
advertise_ip:
media_volumes:
```

Optional variables

```
# vars.yml - See vault.yml vars
run_backup:

# vault.yml
ansible_user:
ansible_become_user:
ansible_become_password:

# Backup vars: required when run_backup == true
backup_user:
backup_server:
backup_ssh_port:
backup_path:

plex_claim_token:
```

### Add an inventory

Create an inventory `YAML` file to configure hosts for deployment. The playbook needs a host group named `plex_server`

```yaml
your_role_name:
  children:
    plex_server:
      hosts:
        your_hostname_or_ip_here:
```

## Run Playbook

```
ansible-playbook \
  ./playbook/main.yml \
  -i ./inventories/homelab.yml \
  --private-key=~/.ssh/id_rsa \
  -u remote-user \
  --vault-password-file=/path/to/password.txt
```


## Deploy via Concord

The playbook can be run from [Concord](https://concord.walmartlabs.com)

### Start Concord process via payload

```
SERVER_URL=https://concord-instance.com:8080 ./run.sh
```