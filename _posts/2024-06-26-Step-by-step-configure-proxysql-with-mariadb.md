---
title: "How to Configure ProxySQL with MariaDB on Your Self-Managed Server"
author: arief
date: 2024-06-26 21:57:00 +07:00
categories: [Database, Database Management]
tags: [proxysql, mysql, mariadb, Linux, Ubuntu, VPS, pooling connection ]
---


***ProxySQL*** is a high-performance MySQL proxy that can help manage a master-slave setup effectively. Here's a detailed guide on how to install and configure ProxySQL on Ubuntu 22.04 with a MariaDB/MySQL master-slave setup.

### Prerequisites
- MariaDB/MySQL Master-Slave Setup: Ensure you have a working master-slave replication setup. If not setup you can follow this [article](https://www.tuxnoob.com/posts/Step-by-step-configure-mariadb-master-slave/)
- Ubuntu 22.04: ProxySQL will be installed on a separate Ubuntu server. In this tutorial using ubuntu 22.04 version

For example, the architecture will like this:

![proxysql-architecture](/assets/images/proxysql-architecture.png){: width="600" height="300" }

### Step 1: Install ProxySQL

- Add ProxySQL Repository:

```sh
sudo apt update
sudo apt install -y wget
wget -O - 'https://repo.proxysql.com/ProxySQL/repo_pub_key' | sudo apt-key add -
echo deb https://repo.proxysql.com/ProxySQL/proxysql-2.0.x/ubuntu/ focal main | sudo tee /etc/apt/sources.list.d/proxysql.list
sudo apt update
```

Or you can download manually and install manual without repository:

```sh
curl -O proxysql_2.5.3-ubuntu22_amd64.deb https://github.com/sysown/proxysql/releases/download/v2.6.3/proxysql_2.6.3-ubuntu22_amd64.deb
```

- Install ProxySQL:

```sh
sudo apt install -y proxysql
```

Or if manual install:

```sh
sudo dpkg -i <package_name>
```

- Start and Enable ProxySQL:

```sh
sudo systemctl start proxysql
sudo systemctl enable proxysql
```

### Step 2: Configure ProxySQL

- Login to ProxySQL Admin Interface:

```sh
mysql -u admin -padmin -h 127.0.0.1 -P 6032
```

- Add MySQL Servers:

```sql
-- Add the Master server
INSERT INTO mysql_servers (hostname, port, hostgroup_id) VALUES ('master_server_ip', 3306, 0);

-- Add the Slave server
INSERT INTO mysql_servers (hostname, port, hostgroup_id) VALUES ('slave_server_ip', 3306, 1);
```

- Add Monitoring User:

Create a monitoring user on both the master and slave servers:

```sh
mysql -u root -p
```

```sql
CREATE USER 'monitor'@'%' IDENTIFIED BY 'monitor_password';
GRANT SELECT ON *.* TO 'monitor'@'%';
FLUSH PRIVILEGES;
```

- Add the Monitoring User to ProxySQL:

```sql
INSERT INTO mysql_users (username, password, default_hostgroup) VALUES ('monitor', 'monitor_password', 0);
LOAD MYSQL USERS TO RUNTIME;
SAVE MYSQL USERS TO DISK;
```

- Add Application User to ProxySQL:

Create the application user on both the master and slave servers:

```sh
mysql -u root -p
```

```sql
CREATE USER 'app_user'@'%' IDENTIFIED BY 'app_password';
GRANT ALL PRIVILEGES ON your_database_name.* TO 'app_user'@'%';
FLUSH PRIVILEGES;
```

Add the application user to ProxySQL:

```sql
INSERT INTO mysql_users (username, password, default_hostgroup) VALUES ('app_user', 'app_password', 0);
LOAD MYSQL USERS TO RUNTIME;
SAVE MYSQL USERS TO DISK;
```

- Configure Query Rules:

```sql
-- Route all writes to the master
INSERT INTO mysql_query_rules (rule_id, active, match_pattern, destination_hostgroup) VALUES (1, 1, '^INSERT|^UPDATE|^DELETE|^REPLACE', 0);

-- Route all reads to the slave
INSERT INTO mysql_query_rules (rule_id, active, match_pattern, destination_hostgroup) VALUES (2, 1, '^SELECT', 1);

LOAD MYSQL QUERY RULES TO RUNTIME;
SAVE MYSQL QUERY RULES TO DISK;
```

- Verify Configuration:

```sql
-- Check servers
SELECT * FROM mysql_servers;

-- Check users
SELECT * FROM mysql_users;

-- Check query rules
SELECT * FROM mysql_query_rules;
```

### Step 3: Connect Application to ProxySQL
Update your application configuration to connect to ProxySQL instead of directly to the MySQL servers. Use the following details:

- Hostname: `proxysql_server_ip` <replace your ip proxysql>
- Port: `6033`
- Username: `app_user` <replace your user>
- Password: `app_password` <replace your password>

### Step 4: Test the Setup

- Test Write Operations:

Connect to ProxySQL and perform a write operation. Verify that the write operation is routed to the master.

```sql
mysql -u app_user -papp_password -h proxysql_server_ip -P 6033
```

```sql
USE your_database_name;
INSERT INTO test_table (id) VALUES (1);
```

- Test Read Operations:
Perform a read operation and verify that the read operation is routed to the slave.

```sql
SELECT * FROM test_table;
```

#### Troubleshooting
- Check ProxySQL Logs: ProxySQL logs can be found at `/var/lib/proxysql/proxysql.log`.
- Check MariaDB/MySQL Logs: Check the logs on the master and slave servers for any replication issues.

Following these steps will set up ProxySQL with your MariaDB/MySQL master-slave replication on Ubuntu 22.04, allowing you to effectively manage and balance your database load.