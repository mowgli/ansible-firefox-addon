ansible-firefox-addon
=====================

This Ansible role provides a `firefox_addon` module for installing or uninstalling Firefox addons.

Requirements
------------

  - firefox
  - curl
  - unzip
  - xmllint
  - sed

Currently the `firefox_addon` module has only been tested against Fedora (23) hosts, but in theory should work for all Linux variants.

Arguments
---------

  - url: url of addon page at addons.mozilla.org (required)
  - profile: path of Firefox profile (optional, defaults to path of profile named `default`)
  - state: one of `present`, `absent` (optional, defaults to `present`)

Notes:

  - A Firefox profile named 'default' will be created if it doesn't already exist.
  - If the addon being installed is a 'complete theme' addon, it will be set as the selected theme.

Dependencies
------------

This role is just a container for the `firefox_addon` module, and as such it has no role dependencies.

Installation
------------

Install from Ansible Galaxy by executing the following command:

```
ansible-galaxy install alzadude.firefox-addon
```

Please note that the role `alzadude.firefox-addon` will need to be added to playbooks to make use of the `firefox_addon` module.

Example Playbook
----------------

Save the following configuration into files with the specified names:

**playbook.yml:**
```
- hosts: linux-workstation
  sudo: no

  roles:
    - alzadude.firefox-addon

  tasks:
    - name: Install adblock plus addon
      firefox_addon:
        url: https://addons.mozilla.org/en-US/firefox/addon/adblock-plus
        state: present
```
**hosts:**
```
# Dummy inventory for ansible
linux-workstation ansible_host=localhost ansible_connection=local
```
Then run the playbook with the following command:
```
ansible-playbook -i hosts playbook.yml
```

License
-------

BSD

