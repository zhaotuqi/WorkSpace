FROM centos:centos7
MAINTAINER zhaotuqi <zhaotuqi@gmail.com>
RUN mkdir -p /data/www #&& mkdir -p /usr/local/webserver
ADD ../www/ \
/data/www/
WORKDIR /data/www
RUN rm -rf /etc/yum.repos.d/CentOS-Base.repo
COPY Centos-7.repo /etc/yum.repos.d/CentOS-Base.repo

#安装依赖
RUN yum -y install gcc gcc-c++\
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
ADD nginx-1.19.7.tar.gz /tmp
RUN cd /tmp/nginx-1.19.7 && ./configure --prefix=/etc/nginx && make -j 2 && make install
RUN rm -rf /etc/nginx/conf/nginx.conf
COPY nginx.conf /etc/nginx/conf
ADD conf.d/ /etc/nginx/conf/conf.d 
RUN ln /etc/nginx/sbin/nginx /usr/local/bin/nginx


#用户账号设置
#RUN echo 'root:123465' | chpasswd
#RUN /usr/sbin/sshd-keygen
#RUN /usr/sbin/groupadd oae &&/usr/sbin/useradd -r -m -s /bin/bash -g oae oae && echo "oae ALL=(ALL) ALL" >> /etc/sudoers && echo 'root:123465' | chpasswd

#安装nginx
#RUN yum -y install epel-release
#RUN yum -y install nginx

#开放端口
EXPOSE 80 22 3306 6379
