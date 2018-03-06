# Tryton Provision

Ansible project to provision and deploy a base instance of [Tryton](http://www.tryton.org/)

## Requeriments

This project has been thinked to run in Ubuntu 16.04 (Xenial).

* Ansible 2.1 or last

You can find more information about Ansible [here](http://docs.ansible.com/)

### Ansible Community Roles

Download Ansible community roles:

```sh
ansible-galaxy install -r requirements.yml
```

We use the next roles:

 - [postgresql](https://galaxy.ansible.com/geerlingguy/postgresql/) v1.3.1

# Playbooks

# Sys Admins `playbooks/sys_admins.yml`

This playbook manages the sysadmin users.

**Need user with `sudo` access without password**

Add your `sys_admins` list in your `inventory/hosy_vars/` file.

`sys_admins` is a list of maps. Need tree keys: `name`, `ssh_key` and `state`:

```YAML
# ./inventory/host_vars/local.tryton.org/config.yml
...

sys_admins:
  - name: tryton
    ssh_key: "~/.ssh/id_rsa.pub"
    state: present
  - name: "{{ development_user }}"
    ssh_key: "~/.ssh/id_rsa.pub"
    state: present

...
```

To execute the playbook run:
```
> ansible-playbook playbooks/sys_admins.yml -u root --limit=dev -v
```
Change `root` for your user.

## Usage example

Configure your hosts and group vars:

```yaml
# inventory/group_vars/all.yml

# User name and password for running ansible on host
user: ubuntu

venv_path: "{{ ansible_env.HOME }}/.venv"

postgresql_users:
  - name: ubuntu
    role_attr_flags: CREATEDB

postgresql_databases:
  - name: tryton-db
```

Then run:

```sh
ansible-playbook playbooks/provision.yml -u ubuntu
```

## Development setup

If you need a development environment you can create a [LXC](https://linuxcontainers.org/lxc/introduction/) container to easy create and destroy it.

You can use lxc-scripts to create it:

```sh
lxc-scripts/lxc-create.sh -n tryton-test -h local.tryton.org
```

## Contributing

1. Fork it (<https://github.com/danypr92/tryton-install>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request
