# https://aws.amazon.com/amazon-linux-2
FROM public.ecr.aws/amazonlinux/amazonlinux:2

RUN yum update -y && \
    amazon-linux-extras install -y epel && \
	yum install -y epel-release && \
	yum clean all
	
RUN yum update -y && \
    yum install -y \
	libcurl-devel \
	libuser-devel \
	openssl-devel \
	postgresql-libs \
	rrdtool \
	wget \
	git \
	subversion \
	which \
	tar \
	jq \
	make \
	automake \
	gcc \
	gcc-c++ \
	sqlite \
	sqlite-devel \
	bzip2 && \
	yum clean all
	
RUN yum update -y && \
    yum upgrade -y ca-certificates
