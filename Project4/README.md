# Project 4 -- WEB Stack Implementation (LEMP Stack)

In this project, we will deploy a LEMP stack web application on an AWS Cloud server.
However, LEMP means Linux, Enginx, Mysql, PHP/Python, or Perl. 

LEMP stack is a solution stack used in deploying web applications, unlike LAMP we use Nginx as the web server for hosting web applications. 

## Launch EC2 Instance on Terminal with SSH

In Order to connect to this ec2. we `cd` into the directory containing the downloaded keypair and run the below code. 

`ssh -i isiak_ec2.pem ubuntu@ec2-172-31-44-245.eu-north-1.commute.amazonaws.com`

![ssh-ec2](images/ssh-ec2.png)

First, we update our firewall with `sudo apt update`

![sudo-apt-update](images/sudo-apt-update.png)

`sudo apt upgrade`

After the update, the terminal wants me to upgrade some packages. 

![sudo-apt-upgrade](images/sudo-apt-upgrade.png)

## Installing Nginx Web Server

`sudo apt install nginx`

![install-nginx](images/install-nginx.png)

`sudo systemctl status nginx`

After successful installation, we use this command to check the status of Apache and here it shows running, which means nginx is active and ready to launch our web server.

![systemctl-status](images/systemctl-status.png)

### Configuring Security Group Inbound Rules on Ec2 Instance

In order to access our nginx website locally or from the internet with any public IP address, we create an inbound rule on aws ec2 security group settings and set HTTP rule, port 80 and source 0.0.0.0/0 means from any IP address. 

![http-inboundrules](images/http-inboundrules.png)

`curl http://localhost:80`

To access our nginx page locally in our Ubuntu shell we use curl `http://localhost:80`

![curl-localhost](images/curl-localhost.png)

`http://<Public-IP-Address>:80`

Here we test how the nginx http server can respond to requests from the internet by opening a web browser and running the ec2 public address. 

![web-nginx](images/web-nginx.png)

## Installing MySQL

MySQL is a Database Management system (DBMS) that stores and manages data for our website in a relational database. 

`sudo apt install mysql-server`

![sudo-apt-install-mysql-server](images/install-mysql-server.png)

`sudo mysql`

This command connects to MySQL server as the administrative database user root

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

![mysql-alsteruser-pass](images/mysql-alsteruser-pass.png)

and with this command, we set a default password for the root user using mysql native password `PassWord.1`

`exit`

then we exit back to our Linux terminal. 

![exit](images/exit.png)

`sudo mysql_secure_installation`

![mysql-secure-ins](images/mysql-secure-inst.png)

![mysql-ins-foot](images/mysql-ins-foot.png)

`sudo mysql -p`

![mysql-p](images/mysql-p.png)

---

## Installing php 

PHP is a component part of our set LEMP stack setup that processes code to display dynamic content to the end user. In addition to the php package, we install `php-mysql` a PHP module that allows PHP to communicate with MySQL database. 
Then we added `php-fpm` which stands for PHP fastCGI process manager. tells Nginx to pass PHP requests to this software for processing.

`sudo apt install php-fpm php-mysql`

![install-php](images/install-php.png)

### Configuring Nginx to Use PHP Processor

Nginx has one server blobk enabled by default and is configured to serve documents out of a directory at `/var/www/html`. While it works well for a single site, it may be hard to manage when hosting multiple sites. So in order not to modifile this `/var/www/html`, we'll create a directory structure within `/var/www` for our domain web. 

`sudo mkdir /var/www/projectLEMP`

Here we created a new directory called `projectLEMP` in `/var/www/`

![mkdir-projectLEMP](images/mkdir-projectLEMP.png)

`sudo chown -R $USER:$USER /var/www/projectLEMP`

Then we assign owner of projectLEMP to current system user.

![chown-projectLEMP](images/chown-projectLEMP.png)

After that, we then create a new config file `projectLEMP` in sites-available directory with 

`sudo nano /etc/nginx/sites-available/projectLEMP`

this command opens a new file, and then we paste the code below inside it ;

`server {

    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}`

![projectLEMP-config](images/projectLEMP-config.png)

After creating the projectLEMP config file in `/etc/nginx/sites-available`, we then link it to `/etc/nginx/sites-enabled` directory.

`sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`

![link-projectLEMP](images/link-projectLEMP.png)

`sudo nginx -t`

This command tests our nginx configuration for syntax errors.

![nginx-t](images/nginx-t.png)

`sudo unlink /etc/nginx/sites-enabled/default`

With this command, we unlink or disable the Nginx default host that is currently configured to listen on port 80. 

`sudo systemctl reload nginx`

Then we reload Nginx.

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`

This command created a new file `index.html` in `/var/www/projectlamp/` also to input some codes in the index.html file. 

![echo-index html](images/echo-index.html.png)

`http://<Public-IP-Address>:80`

Now we check our website with the system browser using the public ip address and it shows what we have in `/var/www/projectlamp/index.html` which is our server public hostname and public ip address

![web-nginx-index html](images/web-nginx-index.html.png)

### Testing PHP with Nginx

In order to test PHP with Nginx we created a new file index.php in our web host projectLEMP and then pasted this PHP code 

`<?php
phpinfo();`. 

`nano /var/www/projectLEMP/index.php`

![nano-index-php](images/nano-index.php.png)

`http://`public_IP`/index.php`

![web-php](images/web-php.png)

`sudo rm /var/www/your_domain/index.php`

## Retrieving Data from MySQL Database with PHP

In order for Nginx web page to query data from MySQL, we need to create a test database with simple to do list and configure access to it. 

First we connect to MySQL server 

`sudo mysql -p`

![sudo-mysql](images/sudo-mysql.png)

`CREATE DATABASE "Isiak_database"; `

Createdn database in MySQL named `Isiak_database`

![create-database](images/create-database.png)

`CREATE USER 'isiak44'@'%' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

Created a user named `isiak44` with default MySQL password `PassWord.1`

![create-user](images/create-user.png)

`GRANT ALL ON example_database.* TO 'example_user'@'%';`

This command grant user `isiak44` full privileges over `Isiak_database`

![grant-database](images/grant-database.png)

`mysql> exit`

Exit from MySQL to my Ubuntu Terminal. 

![exit](https://github.com/isiak44/RasheedPBL/assets/27869977/42fdbd97-f768-4cde-b2c1-280a459e4645)

`sudo mysql -u isiak44 -p`

This command logged into the new user isiak44 in MySQL, `-p` promt the user to input password. 

![mysql-u-isiak44](images/mysql-u-isiak44.png)

`mysql> SHOW DATABASES;`

![show-database](images/show-database.png)

`CREATE TABLE Isiak_database.todo_list (item_id INT AUTO_INCREMENT,content VARCHAR(255),PRIMARY KEY(item_id));`

Here we created a test table in MySQL named `todo_list`

![create-table](images/create-table.png)

`INSERT INTO Isiak_database.todo_list (content) VALUES ("My first Project is Linux");`

Here we inserted a few rows in todo_list table as shown below.

![inser-into-todolist](images/inser-into-todolist.png)

`SELECT * FROM Isiak_database.todo_list;`

This command confirms that the inputed data is saved. 

![insert-into-todolist2](images/insert-into-todolist2.png)

`sudo nano /var/www/projectLEMP/todo_list.php`

Here we created a `todo_list.php` file that contains php script in our projectLEMP web root which connects to MySQL database and query for content in our todo_list table. 

![nano-todo-list](images/nano-todo-list.png)

After saving the php script, we then test the script by inputting the below code on our web browser. 

`http://<Public_IP/todo_list.php`

![web-todo-list](images/web-todo-list.png)

And here we have our test table on MySQL displayed on browser. 

---

### Challenges encountered in this project

Had a challenge with hosting PHP page on Nginx, I keep getting error whenever i launched my index.php on my webserver. 

In order to fix this error, I had to modify the version of php on my ProjectLEMP config file in `/etc/nginx/sites-available/projectLEMP` from `php8.1` to the current php version which is `php7.4`

![error-fixed](images/error-fixed.png)