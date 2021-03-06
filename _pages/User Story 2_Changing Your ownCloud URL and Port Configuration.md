---
layout: default
title:  "user accounts"
permalink: /URL/
---

## User Story 2: Changing Your ownCloud URL and Port Configuration  
ownCloud server is accessible under the route `/owncloud` (which is the default, e.g. <https://example.com/owncloud>). However, you can change this in your web server configuration, by changing the URL from <https://example.com/owncloud> to <https://example.com/>).  

### Config.php Parameters    
To control server operations, ownCloud uses the **config/config.php file**. **config/config.sample.php** lists all the configurable parameters within ownCloud, along with example or default values.  

>**Note**: You do not need to copy everything from **config/config.sample.php**. Add only the parameters you wish to modify.  

To do the changes on Debian/Ubuntu Linux operating systems, you need to edit these files:
-	/etc/apache2/sites-enabled/owncloud.conf  
-	/var/www/owncloud/config/config.php  

### Default Parameters   
Once **config.php** file has been configured by the ownCloud server, you can customize the default values of the given parameters.  

Mentioned below are the default parameters configured by the ownCloud installer and are required by your ownCloud server to operate. 

    'instanceid' => '',
A valid **instanceid** is auto-generated by the ownCloud installer once you install ownCloud.  

    'passwordsalt' => '',
The salt is used to hash all passwords and is auto-generated by the ownCloud installer. Do remember, if you lose this salt you lose all your passwords.  

    'trusted_domains' =>
      array (
        'demo.example.org',
        'otherdomain.example.org',
      ),
This gives a list of trusted domains that users can log into. Specifying trusted domains prevents host header poisoning. You are not supposed to remove this, as it performs necessary security checks.

    'datadirectory' => '/var/www/owncloud/data',
This defines the location of the user files **data/** in the ownCloud directory.

    'version' => '',
Identifies the current version number of your ownCloud installation. This is set up and updated during installation, and so it does not require any changes.

    'dbtype' => 'mysql',
Identifies the database used with this installation.  

    'dbhost' => '',  
This defines the host server name, for example **localhost**, **hostname**, **hostname.example.com**, or the **IP address**. To specify a port use **hostname:####**  
For example,
    
    'dbhost' => 'x.x.x.x:8080',
where x.x.x.x is server’s IP address  
                 
    'dbname' => 'owncloud',      
Defines the name of the ownCloud database, which is set during installation. 

    'dbuser' => '',
Defines the user that ownCloud uses to write to the database. This must be unique across ownCloud instances using the same SQL database.

    'dbpassword' => '',
Defines the password for the database user, which is set up during installation.
  
    'dbtableprefix' => '',
Prefix for the ownCloud tables in the database.

    'installed' => false,
Indicates whether the ownCloud instance was installed successfully; **true** indicates a successful installation, and **false** indicates an unsuccessful installation.    

### Default config.php Example
This is how your config.php will look like after installing ownCloud using MySQL database.

    <?php
    $CONFIG = array (
      'instanceid' => 'oc8c0fd71e03',
      'passwordsalt' => '515a13302a6b3950a9d0fdb970191a',
      'trusted_domains' =>
      array (
        0 => 'localhost',
        1 => 'studio',
        2 => '192.168.10.155'
      ),
      'datadirectory' => '/var/www/owncloud/data',
      'dbtype' => 'mysql',
       'version' => '7.0.2.1',
      'dbname' => 'owncloud',
      'dbhost' => 'localhost',
      'dbtableprefix' => 'oc_',
      'dbuser' => 'oc_carla',
      'dbpassword' => '67336bcdf7630dd80b2b81a413d07',
      'installed' => true,
    );  
    
Once the changes are made and all the files have been saved, restart the Apache server. You can now access ownCloud from either, <https://example.com/> or <https://localhost/>.  

### Proxy Configurations  
The automatic hostname, protocol or webroot detection of ownCloud can fail in certain reverse proxy situations. This configuration allows the automatic detection to be manually overridden. You can find the detailed explanation in the [Overwrite Parameters]( https://doc.owncloud.org/server/10.0/admin_manual/configuration/server/reverse_proxy_configuration.html#overwrite-parameters) section.  

    'overwritehost' => '',
This option allows you to manually override the automatic detection; for example **www.example.com**, or specify the port **www.example.com:8080**.

    'overwriteprotocol' => '',  
When generating URLs, ownCloud attempts to detect whether the server is accessed via **https** or **http**. However, if ownCloud is behind a proxy and the proxy handles the **https** calls, ownCloud would not know that **ssl** is in use, which would result in incorrect URLs being generated.  

    'overwritewebroot' => '',
ownCloud attempts to detect the webroot for generating URLs automatically.
For example, if **www.example.com/owncloud** is the URL pointing to the ownCloud instance, the webroot is **/owncloud**. When proxies are in use, it may be difficult for ownCloud to detect this parameter, resulting in invalid URLs.

    'overwritecondaddr' => '',
This option allows you to define a manual override condition as a regular expression for the remote IP address. For example, defining a range of IP addresses starting with **10.0.0.** and ending with 1 to 3: **^10\.0\.0\.[1-3]$**

    'overwrite.cli.url' => '',
Use this configuration parameter to specify the base URL for any URLs which are generated within ownCloud using any kind of command line tools (cron or occ). The value should contain the full base URL: **https://www.example.com/owncloud**
