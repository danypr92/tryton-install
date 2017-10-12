# Tryton Provision

Ansible project to provision and deploy a base instance of [Tryton](http://www.tryton.org/)

## Requeriments

This project has been thinked to run in Ubuntu 16.04 (Xenial).

* Ansible 2.1 or last

You can find more information about Ansible [here](http://docs.ansible.com/)

## Usage example

Download community roles:

```sh
bin/setup.sh
```

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

## Release History

## Meta

## Contributing

1. Fork it (<https://github.com/danypr92/tryton-install>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request
