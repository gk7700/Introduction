## Introduction 

This quick start guide describes the system requirements and also explains how to install and configure an ownCloud server.
Understanding and ensuring your system meets all of the described prerequisites before you begin installing the product will help ensure a successful outcome.

Before installing the application for the first time, ensure that you have root privileges for the servers and the software described in the table below has already been installed and configured.  

>Note: At the time of writing this manual, version 10.1 is the latest stable version of ownCloud server.

## Prerequisites 

The following requirements must be met for the installation:

Type | Specifications
----- | ---------------
Operating System	| Ubuntu 16.04 and 18.04 <br> Debian 7, 8, and 9 <br> SUSE Linux Enterprise Server 12 with SP1, SP2, and SP3 <br> Red Hat Enterprise Linux/Centos 6.9, 7.3, 7.4, and 7.5 <br> Fedora 27, 28, and 29 <br> openSUSE Leap 42.3 and 15
Database | MySQL or MariaDB 5.5+ <br> Oracle 11g <br> PostgreSQL 9 (versions 10 and above are not yet supported) <br> SQLite
Web server | Apache 2.4 with `prefork` and `mod_php`
PHP Runtime | 5.6, 7.0, 7.1, and 7.2
Server | Debian 7 and 8 <br> SUSE Linux Enterprise Server 12 and 12 SP1 <br> Red Hat Enterprise Linux/Centos 6.5 and 7 (7 is 64-bit only) <br> Ubuntu 14.04 LTS <br> NGINX with PHP-FPM (alternative but unsupported option)
Hypervisors | Hyper-V <br> VMware ESX <br>  Xen <br> KVM
Desktop | Windows 7+ <br> Mac OS X 10.7+ (64-bit only) <br> CentOS 6 and 7 (64-bit only) <br> Ubuntu 16.04, 18.04, and 18.10 <br> Debian 8.0 and 9.0 <br> Fedora 27, 28, and 29 <br> openSUSE Leap 42.3, 15.0, and 15.1
Mobile | iOS 9.0+ <br> Android 4.0+
Web Browser| Edge (current version on Windows 10) <br> IE11+ (except Compatibility Mode) <br> Firefox 57+ or 52 ESR <br> Chrome 66+ <br> Safari 10+
Client Versions | Desktop Client 2.3.3 <br> Android App <br> iOS App
Memory | Minimum of 512 MB

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
