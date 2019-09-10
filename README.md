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
# vault.yml
ansible_user:
ansible_become_user:
ansible_become_password:

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