apt
=========

The apt role can be used to install/uninstall apt packages.

Role Variables
--------------

apt_packages:  # List of apt packages to install / uninstall.

Example Playbook
----------------

- name: Install Apt Packages
  hosts: all
  gather_facts: yes

  roles:
  - role: win_copy
    win_copy:
      src: "{{ baseWindows2012.ec2_config_src }}"
      dest: "{{ baseWindows2012.ec2_config_dest }}"

# Example of destination path format when double quotes in use

  - role: win_copy
    win_copy:
      src: "/tmp/file01"
      dest: "C:\\Temp\\file01.txt"

# Example of destination path format when single quotes in use

  - role: win_copy
    win_copy:
      src: "/tmp/file01"
      dest: "C:\Temp\file01.txt"

Author Information
------------------

Lukasz Ciechanowicz
