FROM jenkins

MAINTAINER jerrychir <jerrychir@163.com>

USER root
#清除了基础镜像设置的源，切换成腾讯云的jessie源
#使用非腾讯云环境的需要将 tencentyun 改为 aliyun
RUN echo '' > /etc/apt/sources.list.d/jessie-backports.list \
    && echo "deb http://mirrors.tencentyun.com/debian jessie main contrib non-free" > /etc/apt/sources.list \
    && echo "deb http://mirrors.tencentyun.com/debian jessie-updates main contrib non-free" >> /etc/apt/sources.list \
    && echo "deb http://mirrors.tencentyun.com/debian-security jessie/updates main contrib non-free" >> /etc/apt/sources.list
#更新源并安装缺少的包
RUN apt-get update && apt-get install -y libltdl7 && apt-get update

ARG dockerGid=999

RUN echo "docker:x:${dockerGid}:jenkins" >> /etc/group 

# 安装 docker-compose 因为等下构建环境的需要
RUN curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

RUN chmod +x /usr/local/bin/docker-compose