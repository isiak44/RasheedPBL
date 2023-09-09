# Project 3 -- Lamp Stack Implemntation

In this project, we will deploy a LAMP stack web application on AWS Cloud server.
However, LAMP means Linux, Apache, Mysql, and PHP/Python or Perl. 

---

## EC2 Instance on AWS

First we created an ubutu linux operating system on our AWS server which is also called ec2 as shown below

![ec2_ubuntu](https://github.com/isiak44/RasheedPBL/assets/27869977/267466ae-0bac-4ac9-a33f-797793b552d1)

In Order to connect to this ec2. we use the ssh and private key pair which is in my download folder. 

`ssh -i isiak_ec2.pem ubuntu@ec2-13-53-106-58.eu-north-1.commute.amazonaws.com`

Running this ssh code on our terminal helps us connect to the ubuntu linux operating system we created on our aws server. 

![ssh-i-isiak_ec2 pem](https://github.com/isiak44/RasheedPBL/assets/27869977/e8b80da4-5236-4fef-82d3-b4dcc5e7455f)

`sudo chmod 0400 <private-key-name>.pem`

Then we change permission for the private key downloaded 

![chmod400-Isiak_ec2 pem](https://github.com/isiak44/RasheedPBL/assets/27869977/6584e65e-8575-4699-bf54-49bc543edb7d)

## Installing Apache and Updating Firewall

First we update our firewall with `sudo apt update`
`sudo apt update`

![sudo-apt-update](https://github.com/isiak44/RasheedPBL/assets/27869977/9d1b37a0-4de6-483c-9597-2f986a412b02)

`sudo apt upgrade`

After the update, the terminal wants me to upgrade some packages. 

![sudo-apt-upgrade](https://github.com/isiak44/RasheedPBL/assets/27869977/18984528-e980-4983-8445-ee9f855bbe4f)

`sudo apt install apache2`

In order to Deployour website, we install apache with the ubuntu package manager `apt`

![sudo-install-apache2](https://github.com/isiak44/RasheedPBL/assets/27869977/073b0a87-c835-436d-b510-00e2a58d394a)

`sudo systemctl status apache2`

After successful installation we use this command to check the status of apache and here it shows running which means apache2 is active and ready to launch our first web server.

![systemctl-status-apache2](https://github.com/isiak44/RasheedPBL/assets/27869977/84c175a8-eb3c-4851-8941-0e409903db16)

### Configuring Security Group Inbound Rules on Ec2 Instance

In order to access our apache website locally from the internet with any public ip address, we create an inbound rule on aws ec2 security group settings and set http rule, port 80 and source 0.0.0.0/0 means from any IP address. 

![Inboundrules](https://github.com/isiak44/RasheedPBL/assets/27869977/f52ac7fa-672f-4e9d-9a58-bc621390020a)

`curl http://localhost:80`

And to access this apache page locally in our ubuntu shell we use curl `http://localhost:80`

![curl-localhost](https://github.com/isiak44/RasheedPBL/assets/27869977/a8ac54f9-ff40-48c2-bb89-5c43ee490dc1)

`http://<Public-IP-Address>:80`

Here we test how Apache http server can respond to requests from the internet by openening a web browser and running the ec2 public address. 

![apace2-default-page](https://github.com/isiak44/RasheedPBL/assets/27869977/ba94d68d-c79b-4408-855f-4569a620f1e6)

## Installing MySQL

MySQL is a Database Management system (DBMS) that stores and manage data for our website in a relational database. 

`sudo apt install mysql-server`

![sudo-apt-install-mysql-server](https://github.com/isiak44/RasheedPBL/assets/27869977/2056a23f-bb0c-4f27-bf73-4c4f9100d813)

`sudo mysql`

This command connect to MySQL server as the administrative database user root

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

and with this command we set a default password for the root user using mysql native password `PassWord.1`

`exit`

then we exit back to our linux terminal. 

![sudo-mysql](https://github.com/isiak44/RasheedPBL/assets/27869977/c2da23a6-e9db-4075-9e24-ca4ea89bb4d2)

`sudo mysql_secure_installation`

![sudo-mysql-secure-installation](https://github.com/isiak44/RasheedPBL/assets/27869977/848ea0a4-7731-46fb-ae20-6f94d944eeff)

Mysql installation footer
![my-sql-installation-footer](https://github.com/isiak44/RasheedPBL/assets/27869977/8f2d47aa-f532-4c5a-837a-9a4c41dba412)

`sudo mysql -p`

![sudo-mysql -p](https://github.com/isiak44/RasheedPBL/assets/27869977/d7b87713-70a3-41ab-bf12-c7b9ee1e1ae8)

## Installing php and its modules

PHP is a component part of our set LAMP stack setup that processes code to display dynamic content to the end user. In addition to the php package, we install `php-mysql` a PHP module that allows PHP to communicate with MySQL database. 
Then we added `libapache2-mod-php` to enable Apache to handle PHP files. To install these 3 packages at once we run

`sudo apt install php libapache2-mod-php php-mysql`

![sudo-apt install-php](https://github.com/isiak44/RasheedPBL/assets/27869977/cca7b7c7-8d69-40c2-a579-96570d9c26ed)

`php -v`

This command prints our php version. 

## Enbling PHP on the website

`sudo vim /etc/apache2/mods-enabled/dir.conf`



![sudo-vim-dir-config](https://github.com/isiak44/RasheedPBL/assets/27869977/fc40710c-0fee-4587-8e4b-66579a59cc4d)

`<IfModule mod_dir.c>
        From this:
        DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>`

![sudo-vim-dir conf](https://github.com/isiak44/RasheedPBL/assets/27869977/3f42bf86-60b1-454a-a210-e98b6089ab48)

`sudo systemctl reload apache2`

After making this changes we reload apache2

![sudo-systemctlreload](https://github.com/isiak44/RasheedPBL/assets/27869977/6fdc71c5-868b-419a-ad01-9b068189bd42)

`vim /var/www/projectlamp/index.php`

Here we created a PHP script to test that PHP is correctly installed and configured on the server.

![Sudo-vim-index php](https://github.com/isiak44/RasheedPBL/assets/27869977/56c11623-8c2d-4fd2-aaa3-8c8c6de98249)

`<?php
phpinfo();`

then we paste the PHP code to the index.php file in projectlamp host. 

`http://<Public-IP-Address>:80`

![php-localhost](https://github.com/isiak44/RasheedPBL/assets/27869977/70cd61d7-be6d-44a8-8bed-172a417cf151)

`$ sudo rm /var/www/projectlamp/index.php`

![rm-index php](https://github.com/isiak44/RasheedPBL/assets/27869977/db68e823-35d4-4cb2-a6b3-ac15093566d7)


## Creating a virtual host for the website using apache

`sudo mkdir /var/www/projectlamp`

![mkdir-projectlamp](https://github.com/isiak44/RasheedPBL/assets/27869977/5a47348d-d5cc-4e21-95e8-eb79dd84e771)


`sudo chown -R $USER:$USER /var/www/projectlamp`

then we assign owner of projectlamp to current system user.

![sudo-chown-R](https://github.com/isiak44/RasheedPBL/assets/27869977/9782d51e-faf9-4d25-a4da-c4bee66868e0)

`sudo vi /etc/apache2/sites-available/projectlamp.conf`

After that we then create an empty file called `projectlamp.conf`

`<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>` 

then we copy this code above to `projectlamp.conf`

![sudo-vim-projectlamp-conf](https://github.com/isiak44/RasheedPBL/assets/27869977/70b9ecc3-2162-401f-bfb5-8a526ee3e0d4)


`sudo ls /etc/apache2/sites-available`.

list of sites available in apache, the 000-default.conf  is the apache configuration while the profjectlamp.conf prompt apache to serve `projectlamp` using `/var/www/projectlamp as its web root directory 

![ls-sites-available](https://github.com/isiak44/RasheedPBL/assets/27869977/abd5c78e-3cda-46f5-9018-c44da10c836d)

`sudo a2ensite projectlamp`

a2ensite command enables the new virtual host "projemplamp.conf"

![sudo-ensite](https://github.com/isiak44/RasheedPBL/assets/27869977/fceec22d-942f-4f51-ae01-2751b9ad292f)

`sudo a2dissite 000-default`

In order for Apache default conf page not to overwrite our new virtual host, we use `a2dissite` to disable apache default page. 

![sudo-a2dissite](https://github.com/isiak44/RasheedPBL/assets/27869977/af0ed5b1-db85-4625-bf94-661da2f1c785)

`sudo apache2ctl configtest`

To make sure the configuration file doesn't contain syntax errors, we use this command to test our conf

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`

This command created a new file `index.html` in `/var/www/projectlamp/` also to input some codes in the index.html file. 

![sudo-echo](https://github.com/isiak44/RasheedPBL/assets/27869977/c55ee24c-ce69-4a01-982c-46b09ab4f2b9)

`http://<Public-IP-Address>:80`

Now we check our website with the system browser using the public ip address and it shows what we have in `/var/www/projectlamp/index.html` which is our server public hostname and public ip address

![echo-localhost](https://github.com/isiak44/RasheedPBL/assets/27869977/7fcec88c-ac93-4c10-be3c-7203ab2cbe5d)
