---
title: "Optimize Your Database: Step-by-Step Guide to Setting Up pgpool-II with PostgreSQL Master-Slave Configuration And Failover Implementation"
author: arief
date: 2024-04-30 15:16:00 +07:00
categories: [Database]
tags: [PostgreSQL, pgpool-II, pgpool2, Failover, Pooling Connection ]
---

![pgpool2](/assets/images/pgpool2-postgresql.png){: .dark }

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_

Pgpool-II is a middleware that sits between PostgreSQL servers and a PostgreSQL database client, providing features like connection pooling, load balancing, automated failover, query caching, and more. It acts as a proxy, managing and distributing client connections across multiple PostgreSQL database servers.

Here's an overview of some key features of pgpool-II:

1. **Connection Pooling:** pgpool-II maintains a pool of established connections to PostgreSQL servers, reducing the overhead of creating and tearing down connections for each client request. This improves performance by minimizing connection setup time and resource usage on the database server.
2. **Load Balancing:** It distributes client connections across multiple PostgreSQL servers to distribute the workload evenly. This helps improve scalability and performance by leveraging the resources of multiple servers.
3. **Automated Failover:** pgpool-II can detect failures of PostgreSQL servers and automatically redirect client connections to standby servers in the event of a primary server failure. This provides high availability and fault tolerance for database applications.
4. **Query Caching:** pgpool-II can cache frequently executed queries and their results, reducing the workload on the database servers and improving query response times for repeated queries.
5. **Parallel Query Execution:** It supports parallel query execution, allowing queries to be distributed and executed concurrently across multiple PostgreSQL servers for faster query processing.
6. **Watchdog:** pgpool-II includes a watchdog feature that monitors the health and status of PostgreSQL servers and pgpool-II instances, performing automated failover and recovery actions as needed to maintain system availability.

Overall, pgpool-II is a powerful tool for improving the performance, scalability, and availability of PostgreSQL database deployments, particularly in environments with high concurrency and demanding workloads. It provides essential features for managing connections, load balancing, and failover, helping developers and administrators build robust and reliable database applications.

The concept will be like in the example below:


![pgpool2](/assets/images/pgpool2-concept.png){: w="700" h="400" }

To setup postgresql replication with pgpool2, it's recommended using the same network to reduce the latency.


Setting up a PostgreSQL cluster with pgpool-II involves several steps, including installing and configuring PostgreSQL, setting up replication between master and slave nodes, and configuring pgpool-II for load balancing and high availability. Here's a step-by-step guide to create a PostgreSQL master-slave setup with pgpool-II:

#### Step 1: Install PostgreSQL

Install PostgreSQL on both the master and slave nodes. You can use your operating system's package manager or download and compile PostgreSQL from source.

If using ubuntu 20.04 above just type:

```
apt install -y postgresql
```

#### Step 2: Configure Master PostgreSQL Server
Edit the postgresql.conf file on the master node to enable replication:

```lua
listen_addresses = 'localhost,192.168.10.11'     # what IP address(es) to listen on;
					                             # comma-separated list of addresses;
					                             # defaults to 'localhost'; use '*' for all
					                             # (change requires restart)
port = 5432				    # (change requires restart)
max_connections = 500	    # (change requires restart)
wal_level = replica         # minimal, replica, or logical
					        # (change requires restart)
wal_log_hints = on          # also do full page writes of non-critical updates
					        # (change requires restart)
wal_compression = on        # enable compression of full-page writes
max_wal_size = 1GB
min_wal_size = 80MB
max_wal_senders = 10        # max number of walsender processes
                            # (change requires restart)
shared_preload_libraries = 'pg_stat_monitor'
pg_stat_monitor.pgsm_query_max_len = 2048
pg_stat_monitor.pgsm_normalized_query = 1
pg_stat_monitor.pgsm_enable_query_plan = yes
```

In above configuration will add `max_wal_size` and `min_wal_size`, enable libraries with `pg_stat_monitor` for monitoring with percona monitoring management.

Edit the `pg_hba.conf` file to allow replication connections from the slave:

```lua
host    replication     `your-user`      192.168.10.12/32          md5
```

*Note: replace the ip address according to your ip address.*
Restart PostgreSQL.

### Step 3: Create a Replication User
Create a replication user on the master server:

```sql
CREATE USER `you-user` REPLICATION LOGIN CONNECTION LIMIT 3 ENCRYPTED PASSWORD 'your-password';
```

### Step 4: Configure Slave PostgreSQL Server

Check socket or service postgreSQL is running or not:

```bash
sudo netstat -anp | grep :5432
sudo systemctl status postgresql
```

If running, should disable running or stop the service before configure the slave.

Copy data directory files from the master:

```bash
cp -pr /var/lib/pgsql/14/data /var/lib/pgsql/14/data_orig
rm -rf /var/lib/pgsql/14/data
```

Change ownership of the postgreSQL directory to match the master:

```bash
chown -R postgres:postgres /var/lib/pgsql
chmod -R 775 /var/lib/pgsql
```

Empty spesific directories on the slave:

```bash
rm -rf /var/lib/pgsql/pg_tablespace_02/*
rm -rf /var/lib/pgsql/pg_tablespace_01/*
rm -rf /var/lib/pgsql/pg_wal/*
```

Take a base backup of the master and restore it on the slave:

```bash
pg_basebackup -h 192.168.10.11 -D /path/to/datadir -U `your-user` -P -v -R -X stream
```

Edit `postgresql.conf` to configure for slave:

```lua
listen_addresses = 'localhost,192.168.10.12'      # what IP address(es) to listen on;
					                            # comma-separated list of addresses;
					                            # defaults to 'localhost'; use '*' for all
					                            # (change requires restart)
port = 5432				                        # (change requires restart)
max_connections = 500			                # (change requires restart)
wal_level = replica         # minimal, replica, or logical
					        # (change requires restart)
wal_compression = on        # enable compression of full-page writes
max_wal_size = 1GB
min_wal_size = 80MB
max_wal_senders = 10        # max number of walsender processes
				            # (change requires restart)
hot_standby = on            # "off" disallows queries during recovery
					        # (change requires restart)
pg_stat_monitor.pgsm_query_max_len = 2048
pg_stat_monitor.pgsm_normalized_query = 1
pg_stat_monitor.pgsm_enable_query_plan = yes
```

Edit the `pg_hba.conf` file to allow replication connections from the master:

```lua
host    replication     'your-user'      192.168.10.11/32           md5
```

Create a `recovery.conf` file in the slave's data directory with the following content:

```lua
standby_mode = on
primary_conninfo = 'host=192.168.10.11 port=5432 user="your-user" password="your-password"'
trigger_file = '/path/to/failover.trigger'
```

Discover how to seamlessly manage replication disruptions in PostgreSQL. Learn the essential steps to resume replication after a master server failure, empowering your slave server to accept writes. You can then fix the master server and turn that into the slave.

Start PostgreSQL on the slave.

### Step 5: Install and Configure pgpool-II

- Install pgpool-II on a separate node (could be the same as the master or slave, but typically it's a dedicated server).
- Configure `pgpool.conf`:
    - Set backend_connection_string to connect to the master and slave nodes.
    - Configure other parameters like listen_addresses, port, etc., according to your setup.

Here, this a few line to configure pgpool-II for postgresql master and slave:

```lua
#------------------------------------------------------------------------------
# CONNECTIONS
#------------------------------------------------------------------------------

# - pgpool Connection Settings -

listen_addresses = '192.168.10.10'
                                   # Host name or IP address to listen on:
                                   # '*' for all, '' for no TCP/IP connections
                                   # (change requires restart)
port = 5432
                                   # Port number
                                   # (change requires restart)
socket_dir = '/var/run/postgresql'
                                   # Unix domain socket path
                                   # The Debian package defaults to
                                   # /var/run/postgresql
                                   # (change requires restart)
listen_backlog_multiplier = 2
                                   # Set the backlog parameter of listen(2) to
                                   # num_init_children * listen_backlog_multiplier.
                                   # (change requires restart)
serialize_accept = off
                                   # whether to serialize accept() call to avoid thundering herd problem
                                   # (change requires restart)
reserved_connections = 0
                                   # Number of reserved connections.
                                   # Pgpool-II does not accept connections if over
                                   # num_init_chidlren - reserved_connections.

# - pgpool Communication Manager Connection Settings -

pcp_listen_addresses = '*'
                                   # Host name or IP address for pcp process to listen on:
                                   # '*' for all, '' for no TCP/IP connections
                                   # (change requires restart)
pcp_port = 9898
                                   # Port number for pcp
                                   # (change requires restart)
pcp_socket_dir = '/var/run/postgresql'
                                   # Unix domain socket path for pcp
                                   # The Debian package defaults to
                                   # /var/run/postgresql
                                   # (change requires restart)

# - Backend Connection Settings -

backend_hostname0 = '192.168.10.11'
                                   # Host name or IP address to connect to for backend 0
backend_port0 = 5432
                                   # Port number for backend 0
backend_weight0 = 1
                                   # Weight for backend 0 (only in load balancing mode)
backend_data_directory0 = '/var/lib/postgresql/main'
                                   # Data directory for backend 0
backend_flag0 = 'ALLOW_TO_FAILOVER'
                                   # Controls various backend behavior
                                   # ALLOW_TO_FAILOVER, DISALLOW_TO_FAILOVER
                                   # or ALWAYS_MASTER
backend_application_name0 = 'postgresql-master.internal'
                                   # walsender's application_name, used for "show pool_nodes" command
backend_hostname1 = '192.168.10.12'
backend_port1 = 5432
backend_weight1 = 1
backend_data_directory1 = '/var/lib/postgresql/standby'
backend_flag1 = 'ALLOW_TO_FAILOVER'
backend_application_name1 = 'postgresql-slave01.internal'

# - Authentication -

enable_pool_hba = on
                                   # Use pool_hba.conf for client authentication
pool_passwd = 'pool_passwd'
                                   # File name of pool_passwd for md5 authentication.
                                   # "" disables pool_passwd.
                                   # (change requires restart)
authentication_timeout = 60
                                   # Delay in seconds to complete client authentication
                                   # 0 means no timeout.

allow_clear_text_frontend_auth = on
                                   # Allow Pgpool-II to use clear text password authentication
                                   # with clients, when pool_passwd does not
                                   # contain the user password

#------------------------------------------------------------------------------
# POOLS
#------------------------------------------------------------------------------

# - Concurrent session and pool size -

num_init_children = 100            # Number of concurrent sessions allowed
                                   # (change requires restart)
max_pool = 10                      # Number of connection pool caches per connection
                                   # (change requires restart)
# - Life time -

child_life_time = 300
                                   # Pool exits after being idle for this many seconds
child_max_connections = 0
                                   # Pool exits after receiving that many connections
                                   # 0 means no exit
connection_life_time = 0
                                   # Connection to backend closes after being idle for this many seconds
                                   # 0 means no close
client_idle_limit = 0
                                   # Client is disconnected after being idle for that many seconds
                                   # (even inside an explicit transactions!)
                                   # 0 means no disconnection

#------------------------------------------------------------------------------
# CONNECTION POOLING
#------------------------------------------------------------------------------

connection_cache = on
                                   # Activate connection pools
                                   # (change requires restart)

                                   # Semicolon separated list of queries
                                   # to be issued at the end of a session
                                   # The default is for 8.3 and later
reset_query_list = 'ABORT; DISCARD ALL'
                                   # The following one is for 8.2 and before
#reset_query_list = 'ABORT; RESET ALL; SET SESSION AUTHORIZATION DEFAULT'


#------------------------------------------------------------------------------
# REPLICATION MODE
#------------------------------------------------------------------------------

replication_mode = off
                                   # Activate replication mode
                                   # (change requires restart)
replicate_select = off
                                   # Replicate SELECT statements
                                   # when in replication mode
                                   # replicate_select is higher priority than
                                   # load_balance_mode.

insert_lock = on
                                   # Automatically locks a dummy row or a table
                                   # with INSERT statements to keep SERIAL data
                                   # consistency
                                   # Without SERIAL, no lock will be issued
lobj_lock_table = ''
                                   # When rewriting lo_creat command in
                                   # replication mode, specify table name to
                                   # lock

# - Degenerate handling -

replication_stop_on_mismatch = off
                                   # On disagreement with the packet kind
                                   # sent from backend, degenerate the node
                                   # which is most likely "minority"
                                   # If off, just force to exit this session

failover_if_affected_tuples_mismatch = off
                                   # On disagreement with the number of affected
                                   # tuples in UPDATE/DELETE queries, then
                                   # degenerate the node which is most likely
                                   # "minority".
                                   # If off, just abort the transaction to
                                   # keep the consistency


#------------------------------------------------------------------------------
# LOAD BALANCING MODE
#------------------------------------------------------------------------------

load_balance_mode = on
                                   # Activate load balancing mode
                                   # (change requires restart)
ignore_leading_white_space = on
                                   # Ignore leading white spaces of each query
white_function_list = ''
                                   # Comma separated list of function names
                                   # that don't write to database
                                   # Regexp are accepted
black_function_list = 'currval,lastval,nextval,setval'
                                   # Comma separated list of function names
                                   # that write to database
                                   # Regexp are accepted

black_query_pattern_list = ''
                                   # Semicolon separated list of query patterns
                                   # that should be sent to primary node
                                   # Regexp are accepted
                                   # valid for streaming replicaton mode only.

database_redirect_preference_list = ''
                                   # comma separated list of pairs of database and node id.
                                   # example: postgres:primary,mydb[0-4]:1,mydb[5-9]:2'
                                   # valid for streaming replicaton mode only.
app_name_redirect_preference_list = ''
                                   # comma separated list of pairs of app name and node id.
                                   # example: 'psql:primary,myapp[0-4]:1,myapp[5-9]:standby'
                                   # valid for streaming replicaton mode only.
allow_sql_comments = off
                                   # if on, ignore SQL comments when judging if load balance or
                                   # query cache is possible.
                                   # If off, SQL comments effectively prevent the judgment
                                   # (pre 3.4 behavior).

disable_load_balance_on_write = 'transaction'
                                   # Load balance behavior when write query is issued
                                   # in an explicit transaction.
                                   # Note that any query not in an explicit transaction
                                   # is not affected by the parameter.
                                   # 'transaction' (the default): if a write query is issued,
                                   # subsequent read queries will not be load balanced
                                   # until the transaction ends.
                                   # 'trans_transaction': if a write query is issued,
                                   # subsequent read queries in an explicit transaction
                                   # will not be load balanced until the session ends.
                                   # 'always': if a write query is issued, read queries will
                                   # not be load balanced until the session ends.

statement_level_load_balance = off
                                   # Enables statement level load balancing

#------------------------------------------------------------------------------
# MASTER/SLAVE MODE
#------------------------------------------------------------------------------

master_slave_mode = on
                                   # Activate master/slave mode
                                   # (change requires restart)
master_slave_sub_mode = 'stream'
                                   # Master/slave sub mode
                                   # Valid values are combinations stream, slony
                                   # or logical. Default is stream.
                                   # (change requires restart)

# - Streaming -

sr_check_period = 0
                                   # Streaming replication check period
                                   # Disabled (0) by default
sr_check_user = 'your-user'
                                   # Streaming replication check user
                                   # This is necessary even if you disable
                                   # streaming replication delay check with
                                   # sr_check_period = 0

sr_check_password = 'your-password'
                                   # Password for streaming replication check user.
                                   # Leaving it empty will make Pgpool-II to first look for the
                                   # Password in pool_passwd file before using the empty password

sr_check_database = 'postgres'
                                   # Database name for streaming replication check
delay_threshold = 0
                                   # Threshold before not dispatching query to standby node
                                   # Unit is in bytes
                                   # Disabled (0) by default

#------------------------------------------------------------------------------
# HEALTH CHECK GLOBAL PARAMETERS
#------------------------------------------------------------------------------

health_check_period = 0
                                   # Health check period
                                   # Disabled (0) by default
health_check_timeout = 20
                                   # Health check timeout
                                   # 0 means no timeout
health_check_user = 'your-user'
                                   # Health check user
health_check_password = 'your-user'
                                   # Password for health check user
                                   # Leaving it empty will make Pgpool-II to first look for the
                                   # Password in pool_passwd file before using the empty password

health_check_database = ''
                                   # Database name for health check. If '', tries 'postgres' frist, then 'template1'

health_check_max_retries = 0
                                   # Maximum number of times to retry a failed health check before giving up.
health_check_retry_delay = 1
                                   # Amount of time to wait (in seconds) between retries.
connect_timeout = 10000
                                   # Timeout value in milliseconds before giving up to connect to backend.
                                   # Default is 10000 ms (10 second). Flaky network user may want to increase
                                   # the value. 0 means no timeout.
                                   # Note that this value is not only used for health check,
                                   # but also for ordinary conection to backend.
```

- Configure pool_hba.conf to allow connections from your applications.

```lua
host	all	    your-user	all	      scram-sha-256
```

- Running to register username with sha25sum

```bash
pg_enc -m -k /var/lib/postgresql/.pgpoolkey -f /etc/pgpool2/pgpool.conf -u your-user -p
```

- Start pgpool-II.

*Note: replace `your-user` and `your-password` to your user and password*

### Step 6: Test the Setup

- Test the replication by inserting data into the master and verifying it's replicated to the slave or for simple test create the database or table.
- Test failover scenarios by shutting down the master node and observing if pgpool-II redirects connections to the slave.
- Test login with remote from database client (Dbeaver etc) to pgpool2 server, for ensure the user has created can login and can show schema or table in postgresql master or slave.


## Additional Tips:
- Monitor the setup regularly to ensure replication is working correctly and pgpool-II is managing connections efficiently.
- Consider setting up monitoring tools like Nagios or Zabbix to receive alerts in case of failures.
- Document your setup thoroughly for easier troubleshooting and future maintenance.
- Keep PostgreSQL or pgpool-II and the operating system updated with the latest security patches and updates.

Following these steps should help you set up a PostgreSQL master-slave setup with pgpool-II for load balancing and high availability. Adjust configurations as needed based on your specific requirements and environment.

