FROM ubuntu-sms-4

# Fix: https://github.com/hadolint/hadolint/wiki/DL4006
# Fix: https://github.com/koalaman/shellcheck/wiki/SC3014
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ARG NB_USER="sagemaker-user"
ARG NB_UID="1000"
ARG NB_GID="100"

ENV NB_USER=$NB_USER \
    NB_UID=$NB_UID \
    NB_GID=$NB_GID \
    HOME=/home/$NB_USER

USER root

RUN apt-get update --fix-missing && \
    apt-get upgrade -yq && \
	apt-get install -yq --no-install-recommends \
	apt-transport-https \
	ca-certificates \
	chromium-browser \
	cmake \
	curl \
	default-jdk \
	dirmngr \
	dpkg-sig \
	file \
	g++ \
	gcc \
	gdal-bin \
	gfortran \
	git \
	gpg \
	gpg-agent \
	gsfonts \
	imagemagick \
	libcairo2-dev \
	libcurl4-openssl-dev \
	libev-dev \
	libfontconfig1-dev \
	libfreetype6-dev \
	libfribidi-dev \
	libgdal-dev \
	libgeos-dev \
	libgl1-mesa-dev \
	libgmp3-dev \
	libharfbuzz-dev \
	libicu-dev \
	libjpeg-dev \
	libmagick++-dev \
	libmysqlclient-dev \
	libopenblas-dev \
	libpaper-utils \
	libpcre2-dev \
	libpng-dev \
	libproj-dev \
	libsodium-dev \
	libssh2-1-dev \
	libssl-dev \
	libtiff-dev \
	libudunits2-dev \
	libv8-dev \
	libxml2-dev \
	locales \
	make \
	pandoc \
	perl \
	qpdf \
	snapd \
	sudo \
	tcl \
	tk \
	tk-dev \
	tk-table \
	tzdata \
	unixodbc-dev \
	unzip \
	vim \
	wget \
	zip \
	zlib1g-dev && \
	rm -rf /var/lib/apt/lists/*
	
ENV TZ America/New_York
RUN export TZ

RUN apt-get update -y && \
    apt-get install -y default-jre default-jdk
	
RUN java -version && \
    javac -version
	
RUN R CMD javareconf

WORKDIR $HOME
USER ${NB_UID}
