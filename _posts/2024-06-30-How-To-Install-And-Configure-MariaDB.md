---
title: "Step-by-Step Guide: Installing and Configuring MariaDB on Ubuntu 22.04"
author: arief
date: 2024-06-30 20:00:00 +07:00
categories: [Infrastructure, Database]
tags: [Ubuntu, Linux, MariaDB]
---


![mailserver](/assets/images/mariadb-ubuntu.png){: width="700" height="550"}

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_

Installing and configuring MariaDB on an Ubuntu 22.04 server is a straightforward process. Below is a step-by-step guide:

### Step 1: Update Your System
Before installing any new packages, it's a good idea to update your system's package list to ensure you have the latest information:

```sh
sudo apt update
sudo apt upgrade -y
```

### Step 2: Install MariaDB
Install the MariaDB server package from the official Ubuntu repositories:

```sh
sudo apt install mariadb-client mariadb-server -y
```

### Step 3: Secure the MariaDB Installation
Run the security script that comes with MariaDB to remove insecure default settings and improve the security of your MariaDB installation:

```sh
sudo mysql_secure_installation
```

You will be prompted to answer several questions:

```sh
mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user. If you've just installed MariaDB, and
haven't set the root password yet, you should just press enter here.

Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password or using the unix_socket ensures that nobody
can log into the MariaDB root user without the proper authorisation.

You already have your root account protected, so you can safely answer 'n'.

Switch to unix_socket authentication [Y/n] Y
Enabled successfully!
Reloading privilege tables..
 ... Success!


You already have your root account protected, so you can safely answer 'n'.

Change the root password? [Y/n] Y
New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] Y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] Y
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] Y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] Y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!
```

### Step 4: Start and Enable MariaDB Service
Ensure that the MariaDB service is started and set to start automatically at boot:

```sh
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

### Step 5: Verify the MariaDB Installation
Log in to the MariaDB shell to verify that the installation was successful:

```sh
sudo mysql -u root -p
```

Enter the root password you set during the secure installation process. You should see a MariaDB prompt.

### Step 6: Create a Database and User
Log in to the MariaDB shell:

```sh
sudo mysql -u root -p
```

Create a new database:

```sql
CREATE DATABASE your_database_name;
Create a new user and grant privileges:
```

```sql
CREATE USER 'your_username'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON your_database_name.* TO 'your_username'@'localhost';
FLUSH PRIVILEGES;
```

Exit the MariaDB shell:

```sql
EXIT;
```

### Step 7: Configure MariaDB (Optional)
Edit the MariaDB configuration file to make additional changes if needed:

```sh
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```

For example, you want expose the ip address so you can remote the database with database client like dbeaver, navicat etc. Replace this value

```plaintext
bind-address            = 127.0.0.1
```

to 

```plaintext
bind-address            = <your-ip-address-server>
```

**Note**: Not recommendation your database change `bind-address` to `0.0.0.0` because security reason.

After making changes, restart the MariaDB service to apply them:

```sh
sudo systemctl restart mariadb
```

### Step 8: Test the Configuration
To test that everything is working as expected, you can log in with the new user and perform some operations:

```sh
mysql -u your_username -p
```

Enter the password for the new user and test with some basic SQL commands:

```sql
USE your_database_name;
SHOW TABLES;
CREATE TABLE test_table (id INT, name VARCHAR(20));
INSERT INTO test_table VALUES (1, 'Test');
SELECT * FROM test_table;
```

This guide should help you successfully install and configure MariaDB on an Ubuntu 22.04 server. If you encounter any issues, refer to the MariaDB documentation or seek assistance from the community.