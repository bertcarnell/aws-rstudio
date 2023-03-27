# https://hub.docker.com/_/ubuntu
#    22.04 LTS
FROM ubuntu:jammy

RUN apt-get update && \
    apt-get install -yq tzdata && \
    ln -fs /usr/share/zoneinfo/America/New_York /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y \
	curl \
	libuser \
	openssl \
	postgresql \
	rrdtool \
	wget \
	git \
	subversion \
	tar \
	jq \
	make \
	automake \
	gcc \
	sqlite3 \
	bzip2
	
RUN apt-get update -y && \
    apt-get install -y linux-aws awscli

