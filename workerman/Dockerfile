##========================================================
## workerman 开发环境
## Version 1.0
##========================================================
FROM ubuntu:14.10

MAINTAINER Yuyou Chow "yuyouchow@gmail.com"

# 安装必要的软件, php, memcached, ssh等
RUN apt-get update
RUN apt-get install -y vim php5 memcached php5-cli git gcc php-pear php5-dev libevent-dev php5-memcached php5-memcache strace lrzsz openssh-server openssh-client

# 安装php的libevent扩展, 提高workerman的性能
RUN pecl channel-update pecl.php.net
RUN pecl install channel://pecl.php.net/libevent-0.1.0
RUN echo extension=libevent.so > /etc/php5/mods-available/libevent.ini
RUN ln -s /etc/php5/mods-available/libevent.ini /etc/php5/cli/conf.d/20-libevent.ini

# 安装php的igbinary扩展, 用于序列化数据, 项目redis采用该序列化器
RUN pecl install channel://pecl.php.net/igbinary-1.2.1
RUN echo extension=igbinary.so > /etc/php5/mods-available/igbinary.ini
RUN ln -s /etc/php5/mods-available/igbinary.ini /etc/php5/cli/conf.d/20-igbinary.ini

# 安装php的inotify扩展, 用于workerman开发环境下检测文件修改并热更
RUN pecl install channel://pecl.php.net/inotify-0.1.6
RUN echo extension=inotify.so > /etc/php5/mods-available/inotify.ini
RUN ln -s /etc/php5/mods-available/inotify.ini /etc/php5/cli/conf.d/20-inotify.ini

# 安装php的redis扩展, 用于访问redis数据库
RUN cd /tmp && git clone https://github.com/phpredis/phpredis.git
RUN cd /tmp/phpredis && phpize && ./configure --enable-redis-igbinary && make && make install
RUN echo extension=redis.so > /etc/php5/mods-available/redis.ini
RUN ln -s /etc/php5/mods-available/redis.ini /etc/php5/cli/conf.d/20-redis.ini

# 安装php的protobuf扩展, 用于解析protobuf协议
RUN cd /tmp && git clone https://github.com/zyuyou/php-protobuf.git
RUN cd /tmp/php-protobuf && phpize && ./configure && make && make install
RUN echo extension=protobuf.so > /etc/php5/mods-available/protobuf.ini
RUN ln -s /etc/php5/mods-available/protobuf.ini /etc/php5/cli/conf.d/20-protobuf.ini

# 部署sshd服务,用于解决windows环境的cmd杂碎问题
ADD sshd_config /etc/ssh/sshd_config
RUN chmod 644 /etc/ssh/sshd_config
RUN echo "ALL:ALL" >>/etc/hosts.allow

RUN echo 'root:123456' | chpasswd

# 暴露开发常用的端口
EXPOSE 80 81 82 22 21 8080 8001 8002 8003 8004 8005 8006 8007 8008 8009 8010

ENTRYPOINT ["/bin/bash", "-l"]
