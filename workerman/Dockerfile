FROM ubuntu:14.10

MAINTAINER Yuyou Chow "yuyouchow@gmail.com"

RUN apt-get update
RUN apt-get install -y vim php5 memcached php5-cli git gcc php-pear php5-dev libevent-dev php5-memcached php5-memcache strace lrzsz openssh-server openssh-client

RUN pecl channel-update pecl.php.net
RUN pecl install channel://pecl.php.net/libevent-0.1.0
RUN echo extension=libevent.so > /etc/php5/mods-available/libevent.ini
RUN ln -s /etc/php5/mods-available/libevent.ini /etc/php5/cli/conf.d/20-libevent.ini

RUN pecl install channel://pecl.php.net/igbinary-1.2.1
RUN echo extension=igbinary.so > /etc/php5/mods-available/igbinary.ini
RUN ln -s /etc/php5/mods-available/igbinary.ini /etc/php5/cli/conf.d/20-igbinary.ini

RUN pecl install channel://pecl.php.net/inotify-0.1.6
RUN echo extension=inotify.so > /etc/php5/mods-available/inotify.ini
RUN ln -s /etc/php5/mods-available/inotify.ini /etc/php5/cli/conf.d/20-inotify.ini

RUN cd /tmp && git clone https://github.com/phpredis/phpredis.git
RUN cd /tmp/phpredis && phpize && ./configure --enable-redis-igbinary && make && make install
RUN echo extension=redis.so > /etc/php5/mods-available/redis.ini
RUN ln -s /etc/php5/mods-available/redis.ini /etc/php5/cli/conf.d/20-redis.ini

RUN cd /tmp && git clone https://github.com/zyuyou/php-protobuf.git
RUN cd /tmp/php-protobuf && phpize && ./configure && make && make install
RUN echo extension=protobuf.so > /etc/php5/mods-available/protobuf.ini
RUN ln -s /etc/php5/mods-available/protobuf.ini /etc/php5/cli/conf.d/20-protobuf.ini

ADD sshd_config /etc/ssh/sshd_config
RUN chmod 644 /etc/ssh/sshd_config
RUN echo "ALL:ALL" >>/etc/hosts.allow

RUN echo 'root:123456' | chpasswd

EXPOSE 80 81 82 22 21 8080 8001 8002 8003 8004 8005 8006 8007 8008 8009 8010

ENTRYPOINT ["/bin/bash", "-l"]
