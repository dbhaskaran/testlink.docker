# Docker Hub Repository:

[![Docker Pulls](https://hub.docker.com/r/bdeepak23/testlink)](https://hub.docker.com/r/bdeepak23/testlink)


https://hub.docker.com/r/bdeepak23/testlink

* Debian 8.8
* testlink 1.9.16
* apache
* dumb-init 1.2.0
* EXPOSE 80
* ENTRYPOINT: /usr/bin/dumb-init
* ENV
  * ENV APACHE_RUN_USER=www-data
  * APACHE_RUN_GROUP=www-data
  * APACHE_LOG_DIR=/var/log/apache2
  * APACHE_PID_FILE=/var/run/apache2.pid
  * APACHE_RUN_DIR=/var/run/apache2
  * APACHE_LOCK_DIR=/var/lock/apache2
  * TERM=xterm
  * TESTLINK_VERSION=1.9.16
  * DUMB_INIT_VERSION=1.2.0


# TestLink in Docker
#### In order to run TestLink Test case management system in a docker container. Follow along:

#### Step 1: Create a docker network for the container to access MySQL DB
```shell
$ sudo docker network create mynetwork
```
#### Step 2: Instantiate a MySQL container
 ```shell
$ docker run -d --name mysql -p 3306:3306 --network mynetwork -v /Users/dockervol/mysql:/var/lib/mysql -e 'MYSQL_ROOT_NAME=root' -e 'MYSQL_ROOT_PASSWORD=password' mysql
```
#### Step 3: Create a database user and grant permissions
```shell
$ docker exec -it mysql bash
```
##### Inside the MySQL container
```shell
$ mysql -uroot -p
```
##### Then run the following commands at the MySQL prompt:
```sql
CREATE DATABASE testlink;
USE testlink;
CREATE USER 'testadmin'@'localhost' IDENTIFIED BY 'password';
GRANT ALL ON *.* TO 'testadmin'@'localhost';
FLUSH PRIVILEGES;
```

#### Step 4: Instantiate the TestLink container
```shell
$ docker run -d -p 80:80 --network mynetwork --name testlink bdeepak23/testlink
```
#### Step 5: You should now be able to access testlink at http://localhost/testlink
