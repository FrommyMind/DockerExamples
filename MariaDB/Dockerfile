#使用的基础镜像
FROM centos/s2i-core-centos7

#添加作者信息
MAINTAINER Daniel Duan


#设置环境变量，便于管理
ENV MARIADB_USER root
ENV MARIADB_PASS 123456
#让容器支持中文
ENV LC_ALL en_US.UTF-8

ADD init/db_init.sh /root/db_init.sh
ADD init/run.sh /root/run.sh

#安装mariadb数据库
RUN yum -y install mariadb-server && \
    yum -y clean all --enablerepo='*' &&  \
    chmod 775 /root/db_init.sh && \
    chmod 775 /root/run.sh && \
    /root/db_init.sh

#对外暴露的端口
EXPOSE 3306

#设置默认启动命令
CMD ["/root/run.sh"]