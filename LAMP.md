# LAMP STACK



**LAMP:** for linux apache mysql python is a stack model component used to build softwares or web apps.

**chmod:** is a command used to change the access mode of a file.

**chown:** is a command used to change the ownership.

**TCP:** stands for transmission transfer protocol. it guarantees that all data will be received in the correct order and without any errors. It establishes 
a connection between two hosts before transmitting data.

**UDP:** stands for user datagram protocol this protocol does not establish a connection before transmitting data and does not guarantee delivery order.
it is used for applications where speed and efficiency are more reliable like streaming.

in contrast tcp is slower than UDP due to the overhead establishing and maintaining connections and the error checking wile UDP is faster and more efficient.

## Part 1 - connect EC2 to powershell

## Part 2 - Installing Apache and updating the firewall

### update a list of packages in package manager
sudo apt update 

### run apache2 package installation
sudo apt install apache2
*To verify that apache2 is running as a service in our OS, we run the following cmd*
* sudo systemctl status apache2 



## Part 3 - install mysql 
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)
* **solution**: mysql -u root -p

## Part 4 - Install PHP
Apache and MySQL are already installed to store and manage your data. php will display the dynamic content to the end user.

To install these 3 packages at once, run the commmand:
* sudo apt install php libapache2-mod-php php-mysql

once done check the version:
* php -v
## Part 5 - Creating a virtual host for your website using apache

Here you will set up a domain called projectlamp, but it can be replaced with any domain of your choice.
Apache on Ubuntu 20.04 has one server block enabled by default that is configured to serve documents from the /var/www/html directory. 
We will leave this configuration as is and will add our own directory next next to the default one.

Create the directory for the projectlamp using 'mkdir' command:
* sudo mkdir /var/www/projectlamp

Next, assign ownership of the directory with the current system user:
* sudo chown -R $USER:$USER /var/www/projectlamp

Then, create and open a new configuration file in Apache's sites-available directory using your preferred command line editor. it can be vim or vi:
- sudo vi /etc/apache2/sites-available/projectlamp.conf

this will create and open the editor in a blank file. copy and paste the text:


 - <VirtualHost *:80>
 
   - ServerName projectlamp
   -ServerAlias www.projectlamp 
   - ServerAdmin webmaster@localhost
   - DocumentRoot /var/www/projectlamp
   - ErrorLog ${APACHE_LOG_DIR}/error.log
   - CustomLog ${APACHE_LOG_DIR}/access.log combined
 
 - </VirtualHost>

save and exit: 
* ESC
* :wq for write and quit

use the command ls to show the new file in the sites-available directory
* sudo ls /etc/apache2/sites-available
![image](https://github.com/Tyannherve11/Devops-Project-1/assets/37128739/8dd116cc-ce8e-4c0d-9d9c-e62c28ec4fe7)

You will get a disable message. to fix that use the command: 
- sudo a2dissite 000-default
To make sure your configuration file doesn’t contain syntax errors, run:
- sudo apache2ctl configtest

Finally, reload apache:
- sudo systemctl reload apache2




