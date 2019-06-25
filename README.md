# Linux-Server-Configuration-Project

### Project Overview 
The last project of Full Stack Web Developer in Udacity. Installation of a Linux server and preparing it to host our web applications.
Securing server from a number of attack vectors, installing and configuring a database server and deploying one of existing web application onto it.

### Why this Project? 
Undestanding of exactly what your web applications are doing, how they are hosted, and the iterations between multiple system are what define 
Full Stack Web Developer. 

### Technical Information 
- **Publicc IP 18.196.31.173
- **User name: ubuntu 
- ** SSH server access port:** 2200

### Get your server
- Start server instance on Amazon Lightsail 

### Create User
- sudo adduser grader
- sudo nano /etc/sudoers.d/grader
- grader ALL=(ALL:ALL) ALL
- sudo nano /etc/hosts

### Configure key for User
- ssh-keygen -t rsa
- ssh-copy-id grader@.......
- cat /.ssh/authorized_keys
- nano /home/grader/.ssh/authorized_keys

### Execute key
- sudo nano/etc/ssh/sshd_congif
- sudo service ssh restart 

### Change port from 22 to 2200
- sudo nano /etc/ssh/sshd_config
- Change port from 22 to 2200 
- Control + X and exit Y 
- sudo service ssh restart

### Update
- sudo apt-get update
- sudo apt-get upgrade

### Create Firewall
- sudo ufw default deny incoming 
- sudo ufw default allow outgoing
- sudo ufw allow 2200/tcp
- sudo ufw allow www
- sudo ufw allow ntp 
- sudo ufw allow enable 

### Install Apache2
- sudo apt-get install apache2 libapache2-mod-wsgi git
- sudo a2enmod wsgi

### Install git 
- sudo apt-get install git
- git config --global user.name <username> git config --global user.email <email> 
  
### Clone project 
- git clone https://github.com/MaciejBec/Project-Item-Catalog.git 
- sudo chmod 777 -R Project-Item-Catalog

### Install PostgresSQL
- sudo apt-get install libpq-dev python-dev
- sudo apt-get install postgresql postgresql-contrib
- sudo cat /etc/postgresql/9.3/main/pg_hba.conf
- sudo su -postgres
- psql 

### Install Dependencies 
- python3 -m venv udacity
- source udacity/bin/acivate
- pip install -r requrements.txt

### Configure Apache 
- sudo nano /etc/apache2/sites-enabled/000-default.conf 

<VirtualHost *:80>
        ServerName 18.196.31.173
        ServerAdmin webmaster@localhost.com
        WSGIDaemonProcess app python-path=/home/grader/Project-Item-Catalog/Udacity/lib/python3.6/site-packages
        WSGIProcessGroup app
        WSGIScriptAlias / /home/grader/Project-Item-Catalog/server.wsgi
        <Directory /home/grader/Project-Item-Catalog/>
                Require all granted
        </Directory>
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>


### Restart Apache
- sudo service apache2 restart
