win_copy
=========

The win_copy role copies a file from the local Ansible build server to remote Windows host.

Role Variables
--------------

win_copy:
  src: '/local/path/file' # Local path to a file to copy to the remote server;
  dest: 'C:\Temp\file.txt' # Remote absolute path where the file should be copied to. If src is a directory, DEST variable must be a directory too.Use \ for path separators or \\ when in "double quotes".

Example Playbook
----------------

- name: Deploy the base configuration to the node
  hosts: ec2_node
  gather_facts: yes

  roles:
  - role: loadvars
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