# Install PostgreSQL 11 on CentOS 7
This guide will help you to install PostgreSQL 11 on CentOS 7. PostgreSQL is the World’s most advanced, powerful, open source relational database system with over 30 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance.

1. Update your system to ensure system packages are up to date.

```
$ sudo yum update -y
```

It is recommended to reboot the system after an update in case the Kernel gets updated.
```
$ sudo reboot
```

2. Add PostgreSQL Yum Repository to your CentOS 7 system.

```
$ sudo yum install https://download.postgresql.org/pub/repos/yum/11/redhat/rhel-7-x86_64/pgdg-centos11-11-2.noarch.rpm
```

Type 'y' and press enter to accept when prompted.

3. Now install PostgreSQL Server / Client packages.

```
$ sudo yum -y install postgresql11-server postgresql11
```

4. Initialize the database and enable automatic start.

```
$ sudo /usr/pgsql-11/bin/postgresql-11-setup initdb

# Success Message
Initializing database ... OK
```

Then start and enable the service to start on boot

```
$ sudo systemctl start postgresql-11
$ sudo systemctl enable postgresql-11
```

> PostgreSQL 11 config file is in /var/lib/pgsql/11/data/postgresql.conf

> In case you have a running Firewall service and remote clients should connect to your database server, allow PostgreSQL service.

```
$ sudo firewall-cmd --add-service=postgresql --permanent
$ sudo firewall-cmd --reload
```

5. Enable remote Acess to PostgreSQL

Edit the file /var/lib/pgsql/11/data/postgresql.conf and set Listen address to your server IP address or “*” for all interfaces.

```
listen_addresses = '192.168.18.9'
```

Also set PostgreSQL to accept remote connections

```
$ sudo vim /var/lib/pgsql/11/data/pg_hba.conf

# Accept from anywhere
host all all 0.0.0.0/0 md5

# Accept from trusted subnet
host all all 192.168.18.0/24 md5
```

Restart the service

```
$ sudo systemctl restart postgresql-11
```

> Set PostgreSQL admin user’s password

```
$ sudo su - postgres 
bash-4.2$ psql -c "alter user postgres with password 'NewStrongPass'"

# Success Message
ALTER ROLE
-bash-4.2$
```

> Create a test user and database

```
-bash-4.2$ createuser test_user
-bash-4.2$ createdb test_db -O test_user
-bash-4.2$ grant all privileges on database test_db to test_user;
```

> Login as a test_user  user try to create a table on the Database.

```
$ psql -U test_user -h localhost -d test_db
```