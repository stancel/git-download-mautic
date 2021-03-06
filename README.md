git-download-mautic
=========

Ansible role that downloads and installs a chosen release of Mautic to the default document root for the Apache webserver.

Requirements
------------

Need to already have MySQL / MariaDB / Percona Server and your webserver (Apache or Nginx) already setup and configured. The defaults assume a Debian based Linux (Ubuntu, Debian, etc.) with a default webserver document root of `/var/www/html` to install the Mautic software. You can override those default variables if that is not the case.

Role Variables
--------------

Choose the git tagged release that you would like to download and install. No default value set.  

```
	git_download_mautic_tagged_release_version: "2.14.1"
```
The default git repo to use when downloading and installing Mautic. This is the default but can be changed if you have a forked/modified git repo that you would prefer to use.  

```
	git_download_mautic_git_repo: "https://github.com/mautic/mautic.git"
```
If you are using your own forked repo an want to use a branch instead of a tagged release then fill in a value and comment out the `tagged_release_version` variable.  Default value is an empty string "".  

```
	git_download_mautic_git_branch: "my-super-special-branch"
```
The database to create when setting up Mautic. The default value is "mautic".  

```
	git_download_mautic_db_name: "mautic"
```
The DB user to create when to be used by the Mautic application. No default value set.  

```
	git_download_mautic_db_user: "mauticDbUser"
```
The password for the DB user being created. No default value set.  

```
	git_download_mautic_db_password: "some-really-secure-password"
```
The root password for your MySQL, MariaDB or Percona Server DB instance to create the DB and user. No default set.

```
	git_download_mautic_mysql_root_password: "your MySQL root password"
```
The Document Root or file path where Mantis files will be stored and served up by your webserver. The default path is `/var/www/html` and assumes you are running Apache2 on Debian or Ubuntu.

First part => *git_download_mautic_web_files_path:* is the root directory of your webserver

Second part =>  *git_download_mautic_web_directory_for_application:* is the application directory inside the root directory

!Be aware of the starting / !

```
    git_download_mautic_web_files_path: "/var/www"
    git_download_mautic_web_directory_for_application: "/html"
```
The linux username used by your webserver. The default value is `www-data` which assumes Apache is used on a Debian or Ubuntu linux.

```
	git_download_mautic_web_user: "www-data"
```
The linux group used by your webserver. The default value is `www-data` which assumes Apache is used on a Debian or Ubuntu linux.

```
	git_download_mautic_web_group: "www-data"
```
Manage package with apt, you can disable the installation of package
```
	manage_packages: true
```

The php.ini configurations, to allow or not the setting of these items, useful if your server is already setup with different values, default are true```
```
	git_download_mautic_configure_mysqli_allow_local_infile: true
	git_download_mautic_configure_memory_limit: true
	git_download_mautic_configure_post_max_size: true
	git_download_mautic_configure_upload_max_filesize: true
	git_download_mautic_configure_max_input_time: true
	git_download_mautic_configure_max_execution_time: true
	git_download_mautic_configure_php_timezone: true
```

Install Composer or not, default is true, disable it if you already have composer installed
```
	git_download_mautic_install_composer: true
```

Is this a "new", "upgrade" or "restore" installation? "new" and "upgrade" installs install files from Git, "restore" skips any git deployments and expect a later role to restore files to the needed directory. Default is "new".
```
	git_download_mautic_installation_type: "new"
```

Is this instance to be used for a "dev", "qa" or "prod" environment? Only "prod" environments will deploy the SuiteCRM schedulers. Default is "prod".
```
	git_download_mautic_environment_type: "prod"
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
	    - stancel.git-download-mautic 


or 


	- hosts: your_marketing_automation_server 
	  vars:
		git_download_mautic_tagged_release_version: "2.14.1"
		git_download_mautic_db_user: "mauticDbUser"
		git_download_mautic_db_password: "some-really-secure-password"
		git_download_mautic_mysql_root_password: "your MySQL root password"
	  roles:
	    - stancel.git-download-mautic

License
-------

GPLv3

Author Information
------------------

[Brad Stancel](https://github.com/stancel) 


