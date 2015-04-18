FROM ubuntu:14.04
MAINTAINER Yuyou Chow "yuyouchow@gmail.com"

RUN apt-get update
RUN apt-get install -y curl make gcc libssl-dev libncurses5-dev

ADD kerl /usr/local/bin/kerl
RUN chmod a+x /usr/local/bin/kerl

RUN kerl update releases
RUN kerl build 17.4 otp-17.4
RUN kerl install otp-17.4 /srv/otp/17.4

RUN echo "source /srv/otp/17.4/activate" >>/root/.bashrc

ENTRYPOINT ["/bin/bash", "-l"]
