git-download-mautic
=========

Ansible role that downloads and installs a chosen release of Mautic to the default document root for the Apache webserver.

Requirements
------------

Need to already have MySQL / MariaDB / Percona Server and your webserver (Apache or Nginx) already setup and configured. The defaults assume a Debian based Linux (Ubuntu, Debian, etc.) with a default webserver document root of `/var/www/html` to install the SuiteCRM software. You can override those default variables if that is not the case.

Role Variables
--------------

Choose the git tagged release that you would like to download and install. No default value set.  

```
	tagged_release_version: "2.13.1"
```
The default git repo to use when downloading and installing Mautic. This is the default but can be changed if you have a forked/modified git repo that you would prefer to use.  

```
	git_repo: "https://github.com/mautic/mautic.git"
```
If you are using your own forked repo an want to use a branch instead of a tagged release then fill in a value and comment out the `tagged_release_version` variable.  Default value is an empty string "".  

```
	git_branch: "my-super-special-branch"
```
The database to create when setting up Mautic. The default value is "mautic".  

```
	db_name: "mautic"
```
The DB user to create when to be used by the Mautic application. No default value set.  

```
	db_user: "mauticDbUser"
```
The password for the DB user being created. No default value set.  

```
	db_password: "some-really-secure-password"
```
The root password for your MySQL, MariaDB or Percona Server DB instance to create the DB and user.  

```
	mysql_root_password: "your MySQL root password"
```
The Document Root or file path where Mantis files will be stored and served up by your webserver. The default path is `/var/www/html` and assumes you are running Apache2 on Debian or Ubuntu.

```
	web_files_path: "/var/www/html"
```
The linux username used by your webserver. The default value is `www-data` which assumes Apache is used on a Debian or Ubuntu linux.

```
	web_user: "www-data"
```
The linux group used by your webserver. The default value is `www-data` which assumes Apache is used on a Debian or Ubuntu linux.

```
	web_group: "www-data"
```
Is this a Mautic Dev or Staging Environment? Cron jobs will not be setup for a Dev environment in case you are importing a database from production and do not want to sync your Mautic integrations from a DEV/QA environment to integrated production systems. The default is "no" 

```
	mautic_dev_env: "no"
```

Dependencies
------------

None

Example Playbook
----------------

	- hosts: your_marketing_automation_server
	  vars_files:
	    - vars/main.yml
	  roles:
	    - { role: stancel.git-download-mautic }


or 


	- hosts: your_marketing_automation_server 
	  vars:
		tagged_release_version: "2.13.1"
		db_user: "mauticDbUser"
		db_password: "some-really-secure-password"
		mysql_root_password: "your MySQL root password"
	  roles:
	    - { role: stancel.git-download-mautic }

License
-------

GPLv3

Author Information
------------------

Brad Stancel
