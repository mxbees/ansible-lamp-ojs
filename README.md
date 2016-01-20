##Ansible Playbook for OJS3 Beta Testing

First, I'd like to mention that [@pesterhazy's LAMP ansible playbook][pesterhazy] was an invaluable resource for guiding me through this process.

The main purpose for this playbook is for my beta testing of [OJS3 by PKP][ojs3]. Given that I'm really not a sysadmin, everytime I wanted to resume my testing, I'd pull from the master branch and... break my install and have to spend *way too much time* troubleshooting. With this playbook, I can just re-provision the box everytime I need to do testing and be sure that I have a clean, up-to-date working instance.

I have no doubt that this playbook could likely be easily adapted for deployment to production environments, since it really doesn't do anything but install a LAMP stack and grab OJS.

##Requirements

This depends on the following bits of software:

- [Vagrant](https://www.vagrantup.com/)
- [Ansible](https://github.com/ansible/ansible)
- [Virtual Box](https://www.virtualbox.org/)

You'll need to install all of these on your local machine before using this playbook (be sure to install the guest additions for virtual box).

##How to use the playbook

1. After installing the above dependencies, clone this repo wherever you'd like to have the shared folder with the virtual machine.
2. Enter in the terminal `vagrant up`.
    (If all goes well, this should do all the necessary work of downloading the box, making the virtual machine, and installing the LAMP stack and OJS.)
3. Once the provisioning has completed, ssh into the machine with `vagrant ssh`.
4. Immediately change directories to the document root: `cd /var/www/html/ojs3/`
5. Copy the config.TEMPLATE.inc.php file, `cp config.TEMPLATE.inc.php config.inc.php`
6. Restart apache. `sudo service apache2 restart`
7. Open a web browser and go to this URL `localhost:8080`
8. This should bring you to the web UI to finish installing OJS. e.g. `http://localhost:8080/index.php/index/install/install`
    - The 'files' directory should be: `/var/www/html/ojs3/files`.
    (If adapting for production, move the files to a non-web accessible directory).
    - The mysql username is `root`.
    - There is no password for root, so leave the field blank. 
    (If adapting for production, you should change this part of the playbook to keep it more secure.)
    - The database name doesn't matter, since you should have the checkbox marked for OJS to create a new database for itself.
    - Pick whatever admin username and password you'd like.
    - You might get a warning that OJS was unable to write to config.inc.php. If you get this screen, copy the config and paste it into over the config.inc.php.
    - And, voila! You should have a working instance of OJS3b.
    
##What's in this repo:

- default: the apache config for the virtual machine. Should change this if you change the document root in playbook.yml.
- playbook.yml: the ansible playbook for provisioning the virtual machine. This is the file you edit if you want add a root password for mysql, and other such things.
- Vagrantfile: the instructions for building the virtual machine. This is the file to change if you want to use a different linux distro. Right now it uses Debian 8.

[pesterhazy]: https://github.com/pesterhazy/vagrant-lamp-ansible
[ojs3]: https://github.com/pkp/ojs
