# Test 1 - Windows IIS Webserver

## Summary
This test requires you to configure a Windows IIS web server using Ansible.  You are provided with two vagrant virtual machines that are able to connecto to one another. One Vagrant vm is an Ubuntu 16.04 box that is pre-configured as an Ansible build server.  From this server, you will run an Ansible playbook that will connect to the second VM and run an Ansible playbook against it.
The second is a Windows 2012R2 Vagrant vm that needs to be configured as an IIS web server.  Details on how this IIS web server should be configured are detailed in the 'Challenges' section below.  You'll use an Ansible playbook to configure this server automatically.  The Ansible playbook has been partially implemented already, so you'll just need to extend it and finish it off.

If you haven't used Vagrant or Ansible before, that's OK.  The tech tests are designed to test a range of skills and experience, starting with basic challenges and working up to more complex ones.  You can find more information on these systems on the [Ansible](https://docs.ansible.com/ansible/intro_getting_started.html) and [Vagrant](https://www.vagrantup.com/intro/index.html) websites.


## Setup
Please follow these steps to set-up the tech-test:
1. Install the following systems if you don't have them:
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads) v5.1.22 or above
- [Vagrant](https://www.vagrantup.com/downloads.html)  v1.9.1 or above

2. Fork this repository then clone your fork to your machine.

3. Launch the Vagrant VMs.  Use the following commands, replacing the 'path to repo' with the path to where you cloned the repository in the pevious step.
```
cd [path to repo]/interview-tech-tests/test1
vagrant up
```
Once the machines are running, you should see two VMs in VirtualBox.  Please run ```vagrant status``` to ensure both VMs are running properly before continuing.  You should see:
```
⇒  vagrant status
Current machine states:

ansible                   running (virtualbox)
winweb                    running (virtualbox)

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
role: Ansible build server

"winweb"
ip: 10.75.75.101
os: Windows 2012R2
role: Windows web server.  Our target node.
```

## Running the playbook
OK, so now we have 2 VMs running.  One Ansible Build server, and one Windows target node.

We now need to run our Ansible playbook on the Ansible Build server which will automatically begin configuring the Windows target node.  The playbook already contains logic to initiate the connection to the target node and execute the windows configuration tasks on it.
Run the following commands to connect to the Ansible build server and run the playbook:
```
# On your local machine
vagrant ssh ansible

# On the ansible VM
cd /vagrant
ansible-playbook -vvvv playbook/playbook.yml
```

You should see the Ansible playbook now execute.  Let this run through, and once complete, your Windows target will have been part configured.  You are now ready to attempt the challenges below.
Once you have implemented some changes, follow the above steps again to re-run the Ansible Playbook.  Ansible is idempotent, so only the change you have made will be applied as it recognises the previous tasks have already been applied.  You can keep re-running the playbook as much as necessary.

To see the changes you have made on the Windows target node, you can click on 'show' in Virtualbox on your local machine which will connect you to the Windows VM (ie. IIS is now installed and an App Pool called 'test1' has been created).
Username/Password is vagrant/vagrant if this is requested.


## Challenges
The following challenges will your experience of Ansible and configuring Windows IIS Web Servers.  It's been designed to be suitable for both beginners who might not have used Ansible before, to more seasoned pros.  We often work with new technologies so being able to adjust and learn quickly is an important skill that we also want to test.

You will be asked to make changes to the Ansible playbook and roles to fully configure a Windows IIS web server.  The beginning of this playbook has been implemented for you but the challenges below, if all complete, will configure it fully as required.  Please complete as many as you can, committing your changes along the way using good Git practices.

#### Challenge 1
Install the ```FileAndStorage-Services``` Windows Feature.

#### Challenge 2
By default, app pools on IIS8 are created to use ManagedRunTime of .NET 4.0.  Please create a second app pool, named 'challenge2', that has its ManagedRunTime attribute set to .NET 2.0.

#### Challenge 3
Using the win_copy role, copy all of the files in the interview-tech-tests/test1/files/ directory to the c:\websites\test1 directory on the target node.

### Challenge 4
Please implement a win_iis_website role and use it to:
1. Delete the default website
2. Deploy a 'test1' website that serves the index.html file in c:\websites\test1.  It can use either of the app pools and should listen to requests on port 80.

The link to module on the Ansible website is here: https://docs.ansible.com/ansible/win_iis_website_module.html


Once you have completed as many of the challenges as you can, please create a Pull Request in GitHub between your fork and the main repo.




#### Footnote: Useful Vagrant Commands
```
vagrant up 			# Starts the Vagrant VMs
vagrant halt 		# Shuts down the vagrant machines.  Saves the state of the VMs
vagrant destroy		# Shuts down and deletes the state of the VMs
```