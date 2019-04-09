# Postgres On Docker
## Overview of Postgres
> According to the offical [Postgres Docs](https://www.postgresql.org/ "Official Postgres Site") it is an open source object-relational database system with over 30 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance.

## Installation and Setup Linux (CentOS 7)
This article assumes that you have installed the Docker setup on your machine and you are ready to go. Click [This Link]() if you need to install docker.


```bash
# Pull the alpine image from docker repository
$ docker pull postgres:alpine

# Confirm image is downloaded
$ docker images

# Start a postgres Instance
$ docker run --name postgres-0 -e POSTGRES_PASSWORD=password -d -p 5432:5432 postgres:alpine

# List out the active containers
$ docker ps

# Bash into the postgres container
$ docker exec -it postgres-0 bash

# Confirm your root location and folders
bash-4.4# pwd
/
bash-4.4# ls
*Root folders here*

# Login to your postgres server
bash-4.4# psql
__You may get an error saying role root does not exist__

bash-4.4# psql -U postgres

# You are now in the postgres instance and can perform any db operations
postgres=#

# Sample psql queries to get you going
#1. Display current user (postgres in our case)
postgres=# \du

#2. Create a test database
postgres=# create database test;
CREATE DATABASE

#3. Connect to your test db
postgres=# \c test
You are now connected to database "test" as user "postgres".
test-# 
```

## Connect to postgres docker container from apps.

> After installing and starting our postgres docker container, you may want to connect to it using an application like **pgadmin3** or from a **different terminal**. Here are the steps.

1. Connect from a different terminal

Make sure you have installed psql on your system before proceeding on with this section

```bash
# Connect to docker container from termminal
$ psql -h localhost -p 5432 -U postgres

Password for user postgres: #Enter your password

psql (11.2)
Type "help" for help.

postgres=# 
```

2. Connect to pgadmin3

Ensure you have pgadmin3 installed in order to follow along.

```bash
# Launch pgadmin3 from terminal or locate it on your sytem and open the app.
$ pgadmin3 &

```