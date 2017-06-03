# Linux-Server-Configuration

## The IP address and SSH port so your server can be accessed by the reviewer.

IP: **34.202.9.158**

Port: **2200**

## The complete URL to your hosted web application.
[http://34.202.9.158/](http://34.202.9.158/)

## A summary of software you installed and configuration changes made.

### Update all installed packages
```
$ sudo apt-get update
$ sudo apt-get upgrade
```

### Setup Uncomplicated Firewall (UFW)
```
$ sudo ufw default deny incoming
$ sudo ufw default allow outgoing
$ sudo ufw allow ssh
$ sudo ufw allow 2200/tcp
$ sudo ufw allow www
$ udo ufw enable
```
### Setup HTTP on port 80 and NTP on port 123

Amazon Lightsail Firewall Settings:

* TCP: 80
* UDP: 123	
* TCP: 2200

### Setup SSH Port on server

``` 
$ nano /etc/ssh/sshd_config

** in file **
# What ports, IPs and protocols we listen for
Port 2200
```

### Disable Password Based Login - Force Key Authentication

``` 
$ nano /etc/ssh/sshd_config

** in file **
# Change to no to disable tunnelled clear text passwords
PasswordAuthentication no
```
### Add User Grader

`$ sudo adduser grader`

### Give Grader Permission to Sudo

``` 
$ sudo touch /etc/sudoers.d/grader
$ sudo nano /etc/sudoers.d/grader

** in file **
grader ALL=(ALL) NOPASSWD:ALL
```

### Create SSH Key for Grader

`$ ssh-keygen`

Saved SSH Key as GraderLogin.pem (private key) and GraderLogin.pub (public key)

### Set Timezone to UTC

`$ sudo dpkg-reconfigure tzdata`

### Install Apache Web Server

`$ sudo apt-get install apache2`

### Install Python mod_wsgi

`$ sudo apt-get install libapache2-mod-wsgi`

### Setup the Apache Config File

`$ sudo nano /etc/apache2/sites-enabled/000-default.conf`

Add the following code:

```
WSGIPythonHome "/usr/local/lib/python2.7/"

WSGIScriptAlias / /var/www/catalog/catalog.wsgi
```

### Install PostgreSQL Database

`$ sudo apt-get install postgresql`

### Create a new User Named Catalog and a new Database named Catalog

`$ sudo postgre`

Created new database _catalog_

Created new user _catalog_

### Install Git

`$ sudo apt-get install git`

### Clone Item Catalog Repository

`$ git clone https://github.com/CharlesMThomas/Game-Catalog.git`


### Install Python PIP Package Manager

`$ sudo apt-get install python-pip`

### Install Python Flask Framework

`$ sudo pip flask`

### Install SQLAlchemy

`$ sudo pip sqlalchemy`

### Install HTTPLib2

`$ pip install httplib2`

### Change User Permissions on .git Folder

`$ sudo chmod 400 .git`


## A list of any third-party resources you made use of to complete this project.

[Linux UFW Setup](https://www.digitalocean.com/community/tutorials/how-to-setup-a-firewall-with-ufw-on-an-ubuntu-and-debian-cloud-server)

[Setting Linux Timezone](https://askubuntu.com/questions/323131/setting-timezone-from-terminal)

[PostgreSQL Create User](https://www.postgresql.org/docs/9.6/static/app-createuser.html)

[PostgreSQL Create Database](https://www.postgresql.org/docs/9.6/static/sql-createdatabase.html)

