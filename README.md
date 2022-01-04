# Ansible Role: Puppet-Agent

[![CI](https://github.com/qs5779/ansible-role-puppet-agent/workflows/CI/badge.svg?event=push)](https://github.com/qs5779/ansible-role-puppet-agent/actions?query=workflow%3ACI)

An Ansible Role that installs [Puppet-agent](https://www.puppet.com) on Linux.

## Requirements

None.

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

    puppet_conf_path: /etc/puppetlabs/puppet/puppet.conf

The path to all the Puppet Labs config file (after the package is installed).

    puppet_agent_config_runinterval: 10800
    puppet_agent_config_environment: production
    puppet_agent_config_certname: "{{ ansible_fqdn }}"

Puppet agent configuration values

    # Used only for Debian/Ubuntu.
        # puppet only provides packages for LTS debian version, we default the dist_codename_deb to the
        #  to the ansible_distribution_release release fact, when installing for example 21.10 impish
        #  override the dist_codename_deb default by setting the var dist_codename_deb to focal via commandline
        #  or playbook.
    dist_codename_deb: "{{ ansible_distribution_release }}"
    puppet_apt_deb: "https://apt.puppetlabs.com/puppet{{ puppet_version }}-release-{{ dist_codename_deb }}.deb"

The .deb file for installation on Debian-based OSes.

    # Used only for RedHat/CentOS.
    puppet_yum_rpm: "https://yum.puppet.com/puppet{{ puppet_version }}-release-el-{{ ansible_distribution_major_version }}.noarch.rpm"

The .rpm file for installation on RedHat-based OSes.

## Dependencies

None.

## Example Playbook

```yaml
---
- hosts: focal.example.net
  roles:
    - { name: qs5779.puppet_agent }
- hosts: impish.example.net
  vars:
    dist_codename_deb: focal
  roles:
    - { name: qs5779.puppet_agent, become: true }
```

## License

MIT

## Author Information

This role was created in 2022 by [Quien Sabe](https://www.quiensabe.org/). It was based on (or plagerized from) the great work of the role authored by [Jeff Geerling](https://github.com/geerlingguy/ansible-role-puppet).
