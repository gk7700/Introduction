## Introduction 

This quick start guide describes the system requirements and also explains how to install and configure an ownCloud server.
Understanding and ensuring your system meets all of the described prerequisites before you begin installing the product will help ensure a successful outcome.

Before installing the application for the first time, ensure that you have root privileges for the servers and the software described in the table below has already been installed and configured.  

>Note: At the time of writing this manual, version 10.1 is the latest stable version of ownCloud server.

## Prerequisites
Following [prerequisites](https://github.com/gk7700/Introduction/blob/master/Installation%20Prerequisites.md) must be met for successful installation and configuration of an ownCloud server. 

### Command Line Installation  
There are different methods and platforms for installing an ownCloud server. However, administrators prefer using the command line over a graphic user interface (GUI). Command line installation involves five steps:

1.	Ensure your server meets the [ownCloud prerequisites](https://doc.owncloud.org/server/10.0/admin_manual/installation/manual_installation.html#prerequisites)  

2.	Once all the prerequisites are met, download and unpack the tarball  

To install ownCloud, first [download the source](https://owncloud.org/download/#instructions-server) (whether community or enterprise) directly from ownCloud, and then unpack the tarball in appropriate directories.  

Once done, set your webserver user to be the owner of your unpacked ownCloud directory.  

	$ sudo chown -R www-data:www-data /var/www/owncloud/

3.	Use the `occ` command to complete the installation process

Use the `occ` command, from the root directory of the ownCloud source, to perform the installation. This removes the need to run the [Graphical Installation Wizard]( https://doc.owncloud.org/server/10.0/admin_manual/installation/installation_wizard.html).

	# Assuming you’ve unpacked the source to /var/www/owncloud/
	$ cd /var/www/owncloud/
	$ sudo -u www-data php occ maintenance:install \
	   --database "mysql" --database-name "owncloud" \
	   --database-user "root" --database-pass "password" \
 	   --admin-user "admin" --admin-pass "password"

>Note: You must run `occ` as your [HTTP user]( >https://doc.owncloud.org/server/10.0/admin_manual/installation/manual_installation.html#set-strong-directory-permissions).

If you want to use a directory other than the default (which is data inside the root ownCloud directory), you can also supply the `--data-dir` switch. For example, if you were using the command above and you wanted the data directory to be `/opt/owncloud/data`, then add `--data-dir/opt/owncloud/data` to the command.

4.	Apply the correct owner and permissions to your ownCloud files and directories
Once the command is executed, apply the [strong directory permissions]( https://doc.owncloud.org/server/10.0/admin_manual/installation/manual_installation.html#set-strong-directory-permissions) to your ownCloud files and directories.

>Note: This is extremely important, as it helps protect your ownCloud installation and ensure that it will operate correctly.

5.	(Optional) post#.installation considerations
