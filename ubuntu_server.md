# Ubuntu Server Basics

Here are some basics that come in handy on an Ubuntu Server box.

## Basic Concepts
### No Root User
While most cloud/slice setups include a root user, Ubuntu is not really designed to use it. Create
a normal user and use "sudo" for everything that requires elevated privileges.

## Setup
### Creating Users
Ubuntu has a shortcut command for creating users called **adduser**

BASH:

	# create the user (andrew):
	sudo adduser andrew
	
	# add to the "sudo" group (instead of the sudoers file)
	usermod -a -G sudo andrew

NOTE: Some servers seem to have the sudo group commented out in **/etc/sudoers** make sure you
uncomment this line:

	# Uncomment to allow members of group sudo to not need a password
	%sudo ALL=NOPASSWD: ALL

## Installing Software

Packages are installed using **apt-get** on Ubuntu. If bash-completion is installed you will
be able to use the tab button to display available packages after typing "apt-get someCommand".
Don't worry about dependencies! Apt-get does a great job of resolving them - I have never had
to track any down manually. Here are a couple of examples:

BASH:

	# you will want to update your apt package information 
	# before installing or upgrading any packages
	sudo apt-get update
	
	# install a package
	sudo apt-get install apache2
	
	# install multiple packages
	sudo apt-get install apache2 php5 mysql-server
	
	# uninstall a package
	sudo apt-get remove apache2
	
	# to update installed packages: first run update to get
	# available package information, then perform the upgrade
	# NOTE: upgrade will prompt you and let you know what it is going to update
	sudo apt-get update
	sudo apt-get upgrade


## Autocomplete

You will want to install the extended bash completion. It even works for listing available packages in apt-get:

BASH:

	sudo apt-get install bash-completion

Then, uncomment the following in /etc/bash.bashrc

	# enable bash completion in interactive shells
	if [ -f /etc/bash_completion ]; then
	    . /etc/bash_completion
	fi

## Change locale to UTF8

Check if en_US.utf8 is listed when you run:

BASH:

	$ locale -a

If not then add by:

BASH:

	sudo localedef --no-archive -i en_US -c -f UTF-8 en_US.UTF-8

Check again:

BASH:

	locale -a

If listed, add to /etc/environment

	LANGUAGE="en_US.utf8"
	LANG="en_US.utf8"

Then reboot server.

## Setting Up Web Server

The packages available via Aptitude are great. Here are the packages that should get a basic LAMP
server up and running.

* mysql-server
* apache2
* php5
* php5-cli
* php5-mysql
* php5-gd
* sendmail
* subversion
* subversion-tools
* rsync
* locate

NOTE: **apachectl** is **apache2ctl** on Ubuntu Server

### Modules
Most apachemodules are installed but not enabled by default. You can find the available modules in
**/etc/apache2/mods-available**. Activated modules are symlinked in **/etc/apache2/mods-enabled**. 
The shortcut command to enable a module is **a2enmod**, and similarly **a2dismod**.

### Virtual Hosts
Ubuntu sets up virtual hosts by default. You will find the configuration files in **/etc/apache2/**
and the docroot in **/var/www**.

Similar to modules, once you have created a virtualhost in **/etc/apache2/sites-available**, you
can enable it by using **a2ensite**, and disable it with **a2dissite**

### Setting up command-line 'mail'

Take a look at [this link] [0]

[0]: http://www.quietearth.us/articles/2006/09/25/Ubuntu-Sending-command-line-mail 