FROM centos:centos7
MAINTAINER zhaotuqi <zhaotuqi@gmail.com>
RUN mkdir -p /data/software && mkdir -p /usr/local/webserver
ADD www/ \
/data/software/
WORKDIR /data/software

#安装依赖
RUN yum -y install wget && \
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
RUN yum makecache && \
yum -y install gcc gcc-c++\
autoconf wget \
psmisc \
openssl openssl-devel \
gperftools-devel \
tar \
passwd \
openssh-server \
openssh-clients \
initscripts \
unzip pcre pcre-devel zlib zlib-devel git \
libxml2 libxml2-devel curl curl-devel \
libjpeg libjpeg-devel libpng libpng-devel freetype freetype-devel \
python-setuptools dos2unix gperf \
libevent libevent-devel bzip2-devel ncurses-devel \
boost libtool boost-devel* libuuid-devel python-sphinx.noarch &&\
yum clean all &&\
rm -rf /var/lib/apt/lists/* &&\
rm -rf /var/cache/yum


#用户账号设置
RUN echo 'root:123465' | chpasswd
RUN /usr/sbin/sshd-keygen
RUN /usr/sbin/groupadd oae &&/usr/sbin/useradd -r -m -s /bin/bash -g oae oae && echo "oae ALL=(ALL) ALL" >> /etc/sudoers && echo 'root:123465' | chpasswd

#安装nginx
RUN yum -y install epel-release
RUN yum -y install nginx

#开放端口
EXPOSE 80 22 3306 6379
