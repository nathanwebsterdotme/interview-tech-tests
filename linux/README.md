# Linux Interview Test

## Summary
This test requires you to configure an Ubuntu server using Ansible.  You are provided with two vagrant virtual machines that are able to connect to one another. One Vagrant vm is an Ubuntu 16.04 box that is pre-configured as an Ansible build server.  From this server, you will run an Ansible playbook that will connect to the second VM and run an Ansible playbook against it.
The second is another Ubuntu 16.04 box that needs to be configured as detailed in the challenges below.  You'll use an Ansible playbook to configure this server automatically.  The Ansible playbook has been partially implemented already, so you'll just need to extend it and finish it off.

If you haven't used Vagrant or Ansible before, that's OK.  The tech tests are designed to test a range of skills and experience, starting with basic challenges and working up to more complex ones.  You can find more information on these systems on the [Ansible](https://docs.ansible.com/ansible/intro_getting_started.html) and [Vagrant](https://www.vagrantup.com/intro/index.html) websites.


## Setup
Please follow these steps to set-up the tech-test:
1. Install the following systems if you don't have them already:
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads) v5.1.22 or above
- [Vagrant](https://www.vagrantup.com/downloads.html)  v1.9.1 or above

2. Fork this repository then clone your fork to your machine.

3. Launch the Vagrant VMs.  Use the following commands, replacing the 'path to repo' with the path to where you cloned the repository in the pevious step.
```
cd [path to repo]/interview-tech-tests/linux
vagrant up
```

Once the machines are running, you should see two VMs in VirtualBox.  Please run ```vagrant status``` to ensure both VMs are running properly before continuing.  You should see:
```
⇒  vagrant status
Current machine states:

ansible                   running (virtualbox)
linuxweb                  running (virtualbox)

This environment represents multiple VMs. The VMs are all listed
above with their current state. For more information about a specific
VM, run `vagrant status NAME`.
```

#### Vagrant VMs Details
Vagrant Machines:

```
"ansible"
ip: 10.75.75.75
os: Ubuntu 16.04
role: Ansible build server.  Where we'll run the playbooks from.

"linuxweb"
ip: 10.75.75.101
os: Ubuntu 16.04
role: Linux web server.  Our target node.
```

## Running the playbook
OK, so now we have 2 VMs running.  One Ansible Build server, and one target node.

We now need to run our Ansible playbook on the Ansible Build server which will automatically begin configuring the target node.  The playbook already contains logic to initiate the connection to the target node and execute the configuration tasks on it.  **You do not need to make any changes to the Vagrantfile.**
Run the following commands to connect to the Ansible build server and run the playbook:
```
# On your local machine
vagrant ssh ansible

# On the ansible VM
cd /vagrant
ansible-playbook -vvvv playbook/playbook.yml
```

You should see the Ansible playbook now execute.  Let this run through, and once complete, your target will have been part configured.  You are now ready to attempt the challenges below.
Once you have implemented some changes, follow the above steps again to re-run the Ansible Playbook.  Ansible is idempotent, so only the change you have made will be applied as it recognises the previous tasks have already been applied.  You can keep re-running the playbook as much as necessary.

To see the changes you have made on the target node, you can ssh to it from your local machine.  Open a new terminal tab and do the following:
```
# On your local machine
vagrant ssh linuxweb
```


## Challenges
The following challenges will test your experience of Ansible and configuring Linux Web Servers.  It's been designed to be suitable for both beginners who might not have used Ansible before, to more seasoned pros.  We often work with new technologies so being able to adjust and learn quickly is an important skill that we also want to test.

You will be asked to make changes to the Ansible playbook and roles to fully configure a basic Nginx web server.  The beginning of this playbook has been implemented for you but the challenges below, if all complete, will configure it fully as required.

**Please complete as many as you can, committing your changes along the way using good Git practices.**

#### Challenge 1
Create a role which allows us to install one or more pip packages.  Use it to install the jinja2 and paramiko pip packages.

#### Challenge 2
Update the apt role so that it can be used to both install and uninstall packages.  Use the updated role to uninstall the 'nano' package.

#### Challenge 3
Create a role to install Nginx and configure it to serve the HTML page found in files/index.html.  This should be served as the default web page.  Nginx must be configured to start automatically when the machine is started.


Once you have completed as many of the challenges as you can, please create a Pull Request in GitHub between your fork and the main repo.



#### Footnote: Useful Vagrant Commands
```
vagrant up    # Starts the Vagrant VMs
vagrant halt    # Shuts down the vagrant machines.  Saves the state of the VMs
vagrant destroy   # Shuts down and deletes the state of the VMs
```
