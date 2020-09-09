本机测试步骤：
运行如下命令：
```
docker run  -v F:\IdeaProjects\DockerExamples\MariaDB\init:/root -it centos/s2i-core-centos7 /bin/bash
```
进入docker后，执行如下命令
yum -y install mariadb-server

export MARIADB_USER=root

export MARIADB_PASS=123456

chmod 775 /root/db_init.sh

/root/db_init.sh

确保每一步都能成功。


build 命令
```
 docker build -t <Docker ID>/mariadb5.5 .
 ```
