# Ansible + Podman HTTPd Container

This automation will deploy a web server via Podman on RHEL systems.  Optionally installs Cockpit as well.

> Supports RHEL 7, 8, and 9 - see Known Issues notes below for RHEL 7 systems.

## Usage

1. Modify the Inventory file to reflect the target hosts in the `http_hosts` group.
2. Provide some variables for RHSM if needed via `rhsm_username` and `rhsm_password` - can also be skipped with the `register_rhsm` tag.  Make sure to Vault those variables if used.
3. Unless the other default variables in `group_vars/all.yml` are modified, it will deploy a UBI HTTPd container via Podman and expose it at port `8080`, mounting the `/opt/www-root` path for serving files.

## Known Issues

- While the automation will deploy all the needed things for RHEL 7 hosts, SystemD and Podman are not compatible due to how old the versions are.  You'll need to manually start the container service by running `/opt/httpdctl.sh start`

## Available Tags

- register_rhsm
- enable_repos
- install_base
- setup_cockpit
- configure_firewalld
- setup_podman
- setup_httpd_container