apt
=========

The apt role can be used to install apt packages.

Role Variables
--------------

apt_packages:  # List of apt packages to install.

Example Playbook
----------------

- name: Install Apt Packages
  hosts: all
  gather_facts: yes

  roles:
  - role: apt
    apt_packages:
      - curl


Author Information
------------------

Apty McAptface
