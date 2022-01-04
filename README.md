# Ansible Role: Puppet-Agent

[![CI](https://github.com/geerlingguy/ansible-role-puppet/workflows/CI/badge.svg?event=push)](https://github.com/geerlingguy/ansible-role-puppet/actions?query=workflow%3ACI)

An Ansible Role that installs [Puppet-agent](https://www.docker.com) on Linux.

## Requirements

Requires Java 7 or later to be installed on the server (you can use the `geerlingguy.java` role to install Java if needed; see the test playbook in `tests/` for an example).

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    puppet_package: puppet-agent
    puppet_version: 7

The package to be installed.

    puppet_service: puppet
    puppet_service_state: stopped
    puppet_service_enabled: false
    puppet_service_manage: false

The service that should be run on this server. By default, this role will not manage a Puppet service, and will not enable it at boot time.

    puppet_bin_path: /opt/puppetlabs/bin

The path to all the Puppet Labs binaries (after the package is installed).

    # Used only for Debian/Ubuntu.
    puppet_apt_deb: "https://apt.puppetlabs.com/puppet{{ puppet_version }}-release-{{ ansible_distribution_release }}.deb"

The .deb file for installation on Debian-based OSes.

    # Used only for RedHat/CentOS.
    puppet_yum_rpm: "https://yum.puppet.com/puppet{{ puppet_version }}-release-el-{{ ansible_distribution_major_version }}.noarch.rpm"

The .rpm file for installation on RedHat-based OSes.

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - qs5779.puppet_agent

## License

MIT

## Author Information

This role was created in 2022 by [Quien Sabe](https://www.quiensabe.org/). It was based on (or plagerized from) the great work of the role authored by [Jeff Geerling](https://github.com/geerlingguy/ansible-role-puppet).
