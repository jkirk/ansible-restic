<p><img src="https://restic.readthedocs.io/en/stable/_static/logo.png" alt="restic logo" title="restic" align="right" height="60" /></p>

# Ansible Role: restic

[![Build Status](https://travis-ci.org/paulfantom/ansible-restic.svg?branch=master)](https://travis-ci.org/paulfantom/ansible-restic)
[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)
[![Ansible Role](https://img.shields.io/badge/ansible%20role-paulfantom.restic-blue.svg)](https://galaxy.ansible.com/paulfantom/restic/)
[![GitHub tag](https://img.shields.io/github/tag/paulfantom/ansible-restic.svg)](https://github.com/paulfantom/ansible-restic/tags)

## Description

Deploy [restic](https://restic.net/) - fast, secure, efficient backup program.

## Requirements

- Ansible > 2.2
- bzip2 installed on deployer machine (same one where ansible is installed)

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `restic_version` | 0.9.2 | restic package version. Also accepts latest as parameter. |
| `restic_user` | "root" | system user to run restic |
| `restic_group` | "root" | system group to run restic |
| `restic_install_path` | "/usr/local/bin" | directory where restic binary will be installed |
| `restic_repos` | [] | restic repositories and cron jobs configuration. More in [defaults/main.yml](defaults/main.yml) |

## Security

To ensure high security this role can allow restic to be run as different user than root and still allowing read-only access to files. This is implemented by following [PR#1483](https://github.com/restic/restic/pull/1483) from restic repository.

## Example

### Playbook

Use it in a playbook as follows:
```yaml
- hosts: all
  become: yes
  roles:
    - paulfantom.restic
```

## Local Testing

The preferred way of locally testing the role is to use Docker and [molecule](https://github.com/metacloud/molecule) (v2.x). You will have to install Docker on your system. See Get started for a Docker package suitable to for your system.
All packages you need to can be specified in one line:
```sh
pip install ansible 'ansible-lint>=3.4.15' 'molecule>2.13.0' docker 'testinfra>=1.7.0' jmespath
```
This should be similar to one listed in `.travis.yml` file in `install` section.
After installing test suit you can run test by running
```sh
molecule test --all
```
For more information about molecule go to their [docs](http://molecule.readthedocs.io/en/latest/).

## Travis CI

Combining molecule and travis CI allows to test how new PRs will behave when used with multiple ansible versions and multiple operating systems. This also allows to create test scenarios for different role configurations. As a result test matrix is quite large and takes more time than local testing, so please be patient.

## Contributing

See [contributor guideline](CONTRIBUTING.md).

## License

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more details.
