+++
title = "Running MySQL on Docker"
description = "Deploying and using a MySQL Docker container"


date = "2017-12-17T20:03:00+03:00"

[taxonomies]
tags = ["howto", "linux", "software"]
categories = ["howto", "linux", "software"]
+++

In Arch Linux, MariaDB is the *default implementation* of MySQL. Today, I found myself in a situation where I needed to run a laravel application that uses the Oracle MySQL. Docker has come in handy in this situation because I already have MariaDB installed in my system. This is post is a quick walk through of how to deploy a MySQL Docker container. You should have Docker installed if you want to follow through.

First pull the MySQL Docker Image by running the command:

```
docker pull mysql/mysql-server:latest
```

With a MySQL image on your machine, run the following command to deploy it:

```
docker run --name sql-container -e MYSQL_ROOT_PASSWORD=my-pass -d mysql/mysql-server:latest
```

This command runs a docker container called "sql-container" with a password: "my-pass". If you ever forget your password, you can see it by ruunning: `docker info sql-container | grep "MYSQL_ROOT_PASSWORD"`.

To log into the container, simply run:

```
docker exec -it sql-container mysql -uroot -p
```

You can obtain any information about your container by running:

```
docker info sql-container
```

In conclusion, using Docker to quickly set up MySQL is painlessly easy and is very convenient.
