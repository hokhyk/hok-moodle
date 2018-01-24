https://en.opensuse.org/SDB:LAMP_setup



This article is updated to reflect the installation in openSUSE Leap 42.2. However it does not deviate much from lower versions of openSUSE.
Getting root access

To get root access, open a terminal and enter the following command:
user $ su -
Password:

After entering a valid password, the prompt should turn red and end with a #.
Setting up Apache2
Installing Apache2

First of all, make sure you have root access and enter the following command:
root # zypper in apache2
Starting Apache2

To start the apache server, enter the following command:
root # systemctl start apache2

If you ever want to restart the apache server, use:
root # systemctl restart apache2

or if you want to stop it
root # systemctl stop apache2

To automatically start the apache server after a reboot:
root # systemctl enable apache2


Testing the installation

To check if you apache server works, use you favorite text editor an create the index.html file in the /srv/www/htdocs/ folder with the following content:

<html><body><h1>Welcome to my web site!</h1></body></html>

Now point your favorite Web browser to: 'localhost'. You should see a page with Welcome to my web site! as a headline.

Index-html.png
Enabling public access to the web server

In this state the web server is only accessible as localhost. If you want to give access to it from a remote host, you have to open port http (=80) in the firewall. To do this, edit the /etc/sysconfig/SuSEfirewall2 file and change the line

FW_CONFIGURATION_EXT=""

into

FW_CONFIGURATION_EXT="apache2""

A space should separate elements in that line

After editing you have to restart the firewall using:
root # systemctl restart SuSEfirewall2

Alternatively, you can do this using YaST and selecting Security and Users --> Firewall --> Allowed services and add HTTP server.
Setting up PHP
Installing PHP7

Make sure you have root access — see above. Install php7 using:
root # zypper in php7 php7-mysql apache2-mod_php7

Don't forget to enable mod-php by executing:
root # a2enmod php7

Your are done, php7 is now installed.
Installing PHP5

If instead you want to install PHP5, the steps are the same as above with 'php5' instead of 'php7':
root # zypper in php5 php5-mysql apache2-mod_php5
root # a2enmod php5

Note you need to choose if to install php7 or php5. You cannot have both of them.
Restarting the webserver

Now that you have installed php, you have to restart the apache2 webserver:
root # systemctl restart apache2
Testing the installation

To verify that php is properly working, create a index.php file into the /srv/www/htdocs/ folder with the following content:

<?php 
phpinfo();
?>

Now, point your browser to 'localhost/index.php'. You should see a page containing a table with all php settings displayed.

Index-php.png
Setting up MariaDB

MariaDB is an alternative package for MySQL, so further on the name mysql is used.
Installing MariaDB

Make sure you have root access — see above. We need to install mariadb and mariadb-tools:
root # zypper in mariadb mariadb-tools

The package mariadb-tools is necessary for administration
Starting the MariaDB server

To start the MariaDB server, execute:
root # systemctl start mysql

If you want to read the messages issued by the server cat the /var/log/messages.
root # cat /var/log/messages

Ensure that the server will start at every boot:
root # systemctl enable mysql

If you ever want to restart mysql, execute
root # systemctl restart mysql

or if you want to stop it
root # systemctl stop mysql

Configuring the MariaDB/MySql server
With Leap 42.1

To configure the MariaDB server with improved security, please use the script 'mysql_secure_installation provided by openSUSE. Hereafter is the description of the full process.
root # mysql_secure_installation
NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB

SERVERS IN PRODUCTION USE! PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current password for the root user. If you've just installed MariaDB, and you haven't set the root password yet, the password will be blank, so you should just press enter here.
Enter current password for root (enter for none):

Just press Enter here.
root #
... (output sequel of previous command)
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB root user without the proper authorisation.
Set root password? [Y/n] y

Just enter y here.
root #
... (output sequel of previous command)
New password:

Enter the password for root now.
root #
... (output sequel of previous command)
Re-enter new password:

Enter the password confirmation.
root #
... (output sequel of previous command)
Password updated successfully!

Reloading privilege tables.. ... Success! By default, a MariaDB installation has an anonymous user, allowing anyone to log into MariaDB without having to have a user account created for them. This is intended only for testing, and to make the installation go a bit smoother. You should remove them before moving into a production environment.
Remove anonymous users? [Y/n]

Answer y to remove anonymous users.
root #
... (output sequel of previous command)
... Success!

Normally, root should only be allowed to connect from 'localhost'. This ensures that someone cannot guess at the root password from the network.
Disallow root login remotely? [Y/n]

Answer y now.
root #
... (output sequel of previous command)
... Success!

By default, MariaDB comes with a database named 'test' that anyone can access. This is also intended only for testing, and should be removed before moving into a production environment.
Remove test database and access to it? [Y/n]

Answer y.
root #
... (output sequel of previous command)
- Dropping test database...

... Success! - Removing privileges on test database... ... Success! Reloading the privilege tables will ensure that all changes made so far will take effect immediately.
Reload privilege tables now? [Y/n]

Answer y.
root #
... (output sequel of previous command)
... Success!

Cleaning up... All done! If you've completed all of the above steps, your MariaDB installation should now be secure.
Thanks for using MariaDB!
For memory in older versions

Replacing <NEW PASSWORD> with the value of the new password your want to define, execute: 

root # mysqladmin -u root password '<NEW PASSWORD>'
Password:

Enter the present password or press only Enter if it has never been defined.
Logging in to the client

Now you can log in into the server client by executing
root # mysql -u root -p
Enter password:

Then give your password.
root #
... (output sequel of previous command)
Welcome to the MariaDB monitor. Commands end with ; or \g.

Your MariaDB connection id is 154 Server version: 10.0.22-MariaDB openSUSE package

Copyright (c) 2000, 2015, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
MariaDB [(none)]>

To go back to the terminal, execute:
root #
... (output sequel of previous command)


Installing phpMyAdmin
What is phpMyAdmin?

phpMyAdmin — a.k.a. pma — is a tool to administrate your databases from a Web interface.
Installing phpMyAdmin

To install phpMyAdmin execute:
root # zypper in phpMyAdmin

This also installs a number of needed php5 modules and restarts the apache2 server.
Logging into phpMyAdmin

To log in to phpMyAdmin:

    Navigate to localhost/phpMyAdmin
    Enter the root username and the root password of your mysql server
    Click on the 'go' button

Normally you should get an error message complaining about the lack of the Multibytes String extension. That is the object of the next section.
Checking phpMyAdmin

Now point your browser at http://localhost/phpMyAdmin/ or http://ip_address/phpMyAdmin/ and enter the mysql root username and its passord.

PhpMyAdminInterface.png

That's all! You can now administer your databases from a Web interface.

You can read the documentation on phpMyAdmin on the phpMyAdmin website.

You should have a working LAMP server now! 
