#Interact with Docker

- Mount Disk
> docker run -it -v ~/.:/opt/project/test-project nginx:1.14.1-alpine bin/sh

- Name a docker and Link two docker
> docker run -it --name nginx nginx:1.14.1-alpine bin/sh
> docker run -it --link xxx:nginx nginx:1.14.1-alpine bin/sh
> # ping nginx

#Mount docker volume
 [Mount](https://ithelp.ithome.com.tw/articles/10207973)

 - Create volumn
 >docker volume create my-vol
 - List volumn
 >docker volume
 - Inspec volumn
 > docker volume inspect my-vol
 - Mount volumn at start
 >docker run -d --name devtest -v myvol2:/app nginx:latest
 - Mount local directory 
 >docker run -d -it --name devtest -v "$(pwd)"/target:/app     nginx:latest
 >docker run -d -it --name mydb -v %TEMP%/target:/app     tsmc/mysql:latest
 # MySQL Statefulset

[Kubernetes – StatefulSets](https://theithollow.com/2019/04/01/kubernetes-statefulsets/)

[Kubernetes Application Management — Stateful Services](https://alibaba-cloud.medium.com/kubernetes-application-management-stateful-services-7825e076bcb3)

M:\Practice>kubectl logs -f -n mytsmcset pod/mysql-0  --previous
error: a container name must be specified for pod mysql-0, choose one of: [mysql xtrabackup] or one of the init containers: [init-mysql clone-mysql]
54m         Normal    Created                  pod/mysql-0         Created container init-mysql
54m         Normal    Started                  pod/mysql-0         Started container init-mysql
54m         Normal    Pulling                  pod/mysql-0         Pulling image "dockeruncer.tsmc.com.tw/dockerhub/ipunktbs/xtrabackup@sha256:febbc078d4ea4dbd327622329ae34d5160b439adf830449a985e1bf0784b66ba"
54m         Normal    Pulled                   pod/mysql-0         Container image "dockeruncer.tsmc.com.tw/dockerhub/mysql@sha256:af74f3efcbc567ed068184b5edf51392dbe8658be1b97f515ec9499f90630649" already present on machine
54m         Normal    Started                  pod/mysql-0         Started container clone-mysql
54m         Normal    Created                  pod/mysql-0         Created container clone-mysql
54m         Normal    Created                  pod/mysql-0         Created container mysql
54m         Normal    Started                  pod/mysql-0         Started container mysql
53m         Normal    Pulled                   pod/mysql-0         Container image "dockeruncer.tsmc.com.tw/dockerhub/ipunktbs/xtrabackup@sha256:febbc078d4ea4dbd327622329ae34d5160b439adf830449a985e1bf0784b66ba" already present on machine
54m         Normal    Pulled                   pod/mysql-0         Successfully pulled image "dockeruncer.tsmc.com.tw/dockerhub/ipunktbs/xtrabackup@sha256:febbc078d4ea4dbd327622329ae34d5160b439adf830449a985e1bf0784b66ba" in 5.672200395s
54m         Normal    Created                  pod/mysql-0         Created container xtrabackup
54m         Normal    Started                  pod/mysql-0         Started container xtrabackup
4m45s       Warning   BackOff                  pod/mysql-0         Back-off restarting failed container


M:\Practice>kubectl logs -f -n mytsmcset pod/mysql-0 -c mysql
2021-04-13 12:19:27+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.0.23-1debian10 started.
2021-04-13 12:19:27+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
2021-04-13 12:19:27+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.0.23-1debian10 started.
2021-04-13T12:19:28.029343Z 0 [System] [MY-010116] [Server] /usr/sbin/mysqld (mysqld 8.0.23) starting as process 1
2021-04-13T12:19:28.061323Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
2021-04-13T12:19:28.332918Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
2021-04-13T12:19:28.438657Z 0 [System] [MY-011323] [Server] X Plugin ready for connections. Bind-address: '::' port: 33060, socket: 
/var/run/mysqld/mysqlx.sock
2021-04-13T12:19:28.548994Z 0 [Warning] [MY-010068] [Server] CA certificate ca.pem is self signed.
2021-04-13T12:19:28.549226Z 0 [System] [MY-013602] [Server] Channel mysql_main configured to support TLS. Encrypted connections are 
now supported for this channel.
2021-04-13T12:19:28.552867Z 0 [Warning] [MY-011810] [Server] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
2021-04-13T12:19:28.606232Z 0 [System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.0.23'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server - GPL.

M:\Practice>kubectl logs -f -n mytsmcset pod/mysql-0 -c xtrabackup
+ cd /var/lib/mysql
+ [[ -f xtrabackup_slave_info ]]
+ [[ -f xtrabackup_binlog_info ]]
+ [[ -f change_master_to.sql.in ]]
+ exec ncat --listen --keep-open --send-only --max-conns=1 3307 -c 'xtrabackup --backup --slave-info --stream=xbstream --host=127.0.0.1 --user=root'
bash: line 36: exec: ncat: not found

# Prepare docker image for mysql backup
[Percona XtraBackup for MySQL Databases](https://www.percona.com/software/mysql-database/percona-xtrabackup)

[Installing Percona XtraBackup from Percona Centos yum repository](https://www.percona.com/doc/percona-xtrabackup/2.4/installation/yum_repo.html)


# Prepare docker image for mysql, nc and db benchmark tool

- Image [mysql-80-centos7 Image](https://hub.docker.com/r/centos/mysql-80-centos7)
- NC installation [How to Install netcat(nc) command on Linux (RedHat/CentOS 7/8) in 5 Easy Steps](https://www.cyberithub.com/install-netcat-command-on-linux/)

> docker pull centos/mysql-80-centos7
- Run database
> docker run -d --name mysql_database -e MYSQL_USER=user -e MYSQL_PASSWORD=pass -e MYSQL_DATABASE=db -p 3306:3306 rhscl/mysql-80-rhel7
> docker run -e MYSQL_USER=user -e MYSQL_PASSWORD=pass -e MYSQL_DATABASE=db -p 3333:3306 centos/mysql-80-centos7:latest

# Percona percona-xtradb-cluster-operator
[percona/percona-xtradb-cluster-operator](https://github.com/percona/percona-xtradb-cluster-operator)

[An Overview of the Percona XtraDB Cluster Kubernetes Operator](https://severalnines.com/database-blog/overview-percona-xtradb-cluster-kubernetes-operator)

# Oracle MySQL operator
[Introducing the Oracle MySQL Operator for Kubernetes](https://blogs.oracle.com/developers/introducing-the-oracle-mysql-operator-for-kubernetes)

