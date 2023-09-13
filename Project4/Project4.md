# Project 4 -- WEB Stack Implemntation (LEMP Stack)
---

In this project, we will deploy a LEMP stack web application on AWS Cloud server.
However, LEMP simply means Linux, Enginx, Mysql, and PHP/Python or Perl. 

## Launch EC2 Instance on Terminal with SSH

In Order to connect to this ec2. we use the ssh and private key pair which is in my download folder. 

`ssh -i isiak_ec2.pem ubuntu@ec2-172-31-44-245.eu-north-1.commute.amazonaws.com`

![ssh-ec2](https://github.com/isiak44/RasheedPBL/assets/27869977/0a590d2c-57dc-4ed1-ad64-dab61b98d6c7)

First we update our firewall with `sudo apt update`

![sudo-apt-update](https://github.com/isiak44/RasheedPBL/assets/27869977/8575f04c-305b-49bb-908f-99eb5bdf73ed)

`sudo apt upgrade`

After the update, the terminal wants me to upgrade some packages. 

![sudo-apt-upgrade](https://github.com/isiak44/RasheedPBL/assets/27869977/eb06aa53-1fdd-482c-a865-0f9cbb3c695a)

---

## Installing Nginx Web Server

`sudo apt install nginx`

![install-nginx](https://github.com/isiak44/RasheedPBL/assets/27869977/28c85586-78a3-40d8-b83a-8caa480bdc0c)

`sudo systemctl status nginx`

After successful installation we use this command to check the status of apache and here it shows running, which means nginx is active and ready to launch our web server.

![systemctl-status](https://github.com/isiak44/RasheedPBL/assets/27869977/c6e0fd1e-8a02-4394-9488-d514217a2cf7)

### Configuring Security Group Inbound Rules on Ec2 Instance

In order to access our nginx website locally or from the internet with any public ip address, we create an inbound rule on aws ec2 security group settings and set http rule, port 80 and source 0.0.0.0/0 means from any IP address. 

![http-inboundrules](https://github.com/isiak44/RasheedPBL/assets/27869977/b2b7a857-c053-47b4-b32d-52d8193ddac4)

`curl http://localhost:80`

And to access our nginx page locally in our ubuntu shell we use curl `http://localhost:80`

![curl-localhost](https://github.com/isiak44/RasheedPBL/assets/27869977/732564c0-58f1-40d3-b5ed-afa46e558fa8)

`http://<Public-IP-Address>:80`

Here we test how nginx http server can respond to requests from the internet by openening a web browser and running the ec2 public address. 

![web-nginx](https://github.com/isiak44/RasheedPBL/assets/27869977/9fd551c2-aa65-4e11-8aaa-a9eed7ce4dbc)

---

## Installing MySQL

MySQL is a Database Management system (DBMS) that stores and manage data for our website in a relational database. 

`sudo apt install mysql-server`

![sudo-apt-install-mysql-server](https://github.com/isiak44/RasheedPBL/assets/27869977/2056a23f-bb0c-4f27-bf73-4c4f9100d813)

`sudo mysql`

This command connect to MySQL server as the administrative database user root

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

![mysql-alsteruser-pass](https://github.com/isiak44/RasheedPBL/assets/27869977/562c079b-8e79-4ce8-949e-b9492f975572)

and with this command we set a default password for the root user using mysql native password `PassWord.1`

`exit`

then we exit back to our linux terminal. 

![exit](https://github.com/isiak44/RasheedPBL/assets/27869977/50c297fa-f37f-4d42-85f2-4256e891cd26)

`sudo mysql_secure_installation`

![mysql-secure-ins](https://github.com/isiak44/RasheedPBL/assets/27869977/2e658a32-a46f-416f-9219-b59075349d73)

![mysql-ins-foot](https://github.com/isiak44/RasheedPBL/assets/27869977/2c867c0b-55fb-4cd8-89ed-b789f871b537)

`sudo mysql -p`

![mysql-p](https://github.com/isiak44/RasheedPBL/assets/27869977/3e565bda-8fdd-469c-b557-54318a42453a)

---

## Installing php 

PHP is a component part of our set LEMP stack setup that processes code to display dynamic content to the end user. In addition to the php package, we install `php-mysql` a PHP module that allows PHP to communicate with MySQL database. 
Then we added `php-fpm` which stands for PHP fastCGI process manager. tells Nginx to pass PHP requests to this software for processing.

`sudo apt install php-fpm php-mysql`

![install-php](https://github.com/isiak44/RasheedPBL/assets/27869977/1f08d8c7-1283-4130-86fd-5afaaa6b84ef)

### Configuring Nginx to Use PHP Processor

Nginx has one server blobk enabled by default and is configured to serve documents out of a directory at `/var/www/html`. While it works well for a single site, it may be hard to manage when hosting multiple sites. So in order not to modifile this `/var/www/html`, we'll create a directory structure within `/var/www` for our domain web. 

`sudo mkdir /var/www/projectLEMP`

Here we created a new directory called `projectLEMP` in `/var/www/`

![mkdir-projectLEMP](https://github.com/isiak44/RasheedPBL/assets/27869977/80fd9bee-7b7f-4b92-a74b-32316d7d9c36)

`sudo chown -R $USER:$USER /var/www/projectLEMP`

then we assign owner of projectLEMP to current system user.

![chown-projectLEMP](https://github.com/isiak44/RasheedPBL/assets/27869977/03fd8a56-34ca-4496-8fc4-a33537175b5d)

After that we then create a new config file `projectLEMP` in sites-available directory with 

`sudo nano /etc/nginx/sites-available/projectLEMP`

this command open a new file, then we paste the code below inside it ;

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

![projectLEMP-config](https://github.com/isiak44/RasheedPBL/assets/27869977/6adeb0d6-a90b-4782-9173-2ff5f83ddd55)

After creating the projectLEMP config fille in sites-available, we then link it to sites-enabled directory.

`sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`

![link-projectLEMP](https://github.com/isiak44/RasheedPBL/assets/27869977/140bb387-0753-4238-ad24-7129b5c799fa)

`sudo nginx -t`

This command test our nginx configuration for syntax errors.

![nginx-t](https://github.com/isiak44/RasheedPBL/assets/27869977/1c44c867-71e6-4ea2-84cc-9514d603ea9e)

`sudo unlink /etc/nginx/sites-enabled/default`

With this command we unlink or disabled Nginx default host that is currently configured to listen on port 80. 

`sudo systemctl reload nginx`

Then we reload Nginx.

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`

This command created a new file `index.html` in `/var/www/projectlamp/` also to input some codes in the index.html file. 

![echo-index html](https://github.com/isiak44/RasheedPBL/assets/27869977/9ed501e9-baf5-4cc8-bb78-177dcc363985)

`http://<Public-IP-Address>:80`

Now we check our website with the system browser using the public ip address and it shows what we have in `/var/www/projectlamp/index.html` which is our server public hostname and public ip address

![web-nginx-index html](https://github.com/isiak44/RasheedPBL/assets/27869977/205493bd-e158-407c-aec8-f8d8d275aebc)

---

### Testing PHP with Nginx

In order to test PHP with Nginx we created a new file index.php in our webhost projectLEMP and then pasted this PHP code 

`<?php
phpinfo();`. 

`nano /var/www/projectLEMP/index.php`

![nano-index php](https://github.com/isiak44/RasheedPBL/assets/27869977/155dd4a1-6d81-44a2-8f19-ff78413cbbf5)

`http://`public_IP`/index.php`

![web-php](https://github.com/isiak44/RasheedPBL/assets/27869977/833fe500-7e39-4662-a428-1e7f72844f69)

`sudo rm /var/www/your_domain/index.php`

---

## Retrieving Data from MySQL Database with PHP

In order for Nginx web page to query data from MySQL, we need to create a test database with simple to do list and configure access to it. 

First we connect to MySQL server 

`sudo mysql -p`

![sudo-mysql](https://github.com/isiak44/RasheedPBL/assets/27869977/250ba894-c684-4bf7-b329-fca70c364e76)

`CREATE DATABASE "Isiak_database"; `

Createdn database in MySQL named `Isiak_database`

![create-database](https://github.com/isiak44/RasheedPBL/assets/27869977/658b24c1-199c-46c4-9c5f-200845247be5)

`CREATE USER 'isiak44'@'%' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

Created a user named `isiak44` with default MySQL password `PassWord.1`

![create-user](https://github.com/isiak44/RasheedPBL/assets/27869977/871e078f-9015-44ca-a9c5-81e5325c7e6f)

`GRANT ALL ON example_database.* TO 'example_user'@'%';`

This command grant user `isiak44` full privileges over `Isiak_database`

![grant-database](https://github.com/isiak44/RasheedPBL/assets/27869977/bda64f66-4d93-464f-b269-a2be6f1286b8)

`mysql> exit`

Exit from MySQL to my Ubuntu Terminal. 

![exit](https://github.com/isiak44/RasheedPBL/assets/27869977/42fdbd97-f768-4cde-b2c1-280a459e4645)

`sudo mysql -u isiak44 -p`

This command logged into the new user isiak44 in MySQL, `-p` promt the user to input password. 

![mysql-u-isiak44](https://github.com/isiak44/RasheedPBL/assets/27869977/cd9df54b-c3aa-4763-a861-5dd6e4c9391b)

`mysql> SHOW DATABASES;`

![show-database](https://github.com/isiak44/RasheedPBL/assets/27869977/1912daeb-be44-431e-b88f-39f909659eb2)

`CREATE TABLE Isiak_database.todo_list (item_id INT AUTO_INCREMENT,content VARCHAR(255),PRIMARY KEY(item_id));`

Here we created a test table in MySQL named `todo_list`

![create-table](https://github.com/isiak44/RasheedPBL/assets/27869977/0611a9e8-8d9f-45d9-a225-8a5c4df0c0bc)

`INSERT INTO Isiak_database.todo_list (content) VALUES ("My first Project is Linux");`

Here we inserted a few rows in todo_list table as shown below.

![inser-into-todolist](https://github.com/isiak44/RasheedPBL/assets/27869977/5a54d89c-a6a3-4664-9d03-fe5d1f62fdb8)

`SELECT * FROM Isiak_database.todo_list;`

This command confirms that the inputed data is saved. 

![insert-into-todolist2](https://github.com/isiak44/RasheedPBL/assets/27869977/09090260-8dc1-460b-9afb-2cd1b4c66118)

`sudo nano /var/www/projectLEMP/todo_list.php`

Here we created a `todo_list.php` file that contains php script in our projectLEMP web root which connects to MySQL database and query for content in our todo_list table. 

![nano-todo-list](https://github.com/isiak44/RasheedPBL/assets/27869977/6947884f-a80c-4345-97a1-3267589534c2)

After saving the php script, we then test the script by inputting the below code on our web browser. 
`http://<Public_IP/todo_list.php`

![web-todo-list](https://github.com/isiak44/RasheedPBL/assets/27869977/e91a6b23-4b97-42e7-a8ae-314ff19f166f)

And here we have our test table on MySQL displayed on browser. 

---

### Challenges encountered in this project

Had a challenge with hosting PHP page on Nginx, I keep getting error whenever i launched my index.php on my webserver. 

In order to fix this error, I had to modify the version of php on my ProjectLEMP config file in `/etc/nginx/sites-available/projectLEMP` from `php8.1` to the current php version which is `php7.4`

![error-fixed](https://github.com/isiak44/RasheedPBL/assets/27869977/a62a6266-8ffb-47d8-8c52-9d12b971cb0a)

