FROM ubuntu:14.04

MAINTAINER Yuyou Chow "yuyouchow@gmail.com"

RUN apt-get update
RUN apt-get install -y vim php5 memcached php5-cli git gcc php-pear php5-dev libevent-dev php5-memcached php5-memcache strace lrzsz openssh-server openssh-client

RUN pecl channel-update pecl.php.net
RUN pecl install channel://pecl.php.net/libevent-0.1.0
RUN echo extension=libevent.so > /etc/php5/cli/conf.d/libevent.ini

ADD sshd_config /etc/ssh/sshd_config
RUN chmod 644 /etc/ssh/sshd_config
RUN echo "ALL:ALL" >>/etc/hosts.allow

RUN echo 'root:123456' | chpasswd

EXPOSE 80 81 82 22 21 8080 8001 8002 8003 8004 8005 8006 8007 8008 8009 8010

ENTRYPOINT ["/bin/bash", "-l"]
