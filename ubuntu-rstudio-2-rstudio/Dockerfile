FROM ubuntu-rstudio-1-system

# https://docs.posit.co/rsw/installation/
#   these directions call for (as of 3/26/2023)
#      curl -O https://download2.rstudio.org/server/jammy/amd64/rstudio-workbench-2023.03.0-386.pro1-amd64.deb
#   but a miniumum of 485 is required
# this page shows the example rhel7 release 
#   https://dailies.rstudio.com/rstudio/prairie-trillium/workbench/centos7/page/2/
# this page shows the release selected here
#   https://dailies.rstudio.com/rstudio/prairie-trillium/workbench/jammy/


RUN apt-get update -y && \
    apt-get install -y gdebi-core

# https://s3.amazonaws.com/rstudio-ide-build/server/jammy/amd64/rstudio-workbench-2022.02.5-503.pro1-amd64.deb
ARG RSW_OS=jammy
ARG RSW_ARCH=amd64
ARG RSW_NAME=rstudio-workbench
ARG RSW_VERSION=2022.02.5-503.pro1
ARG RSW_DOWNLOAD_URL=https://s3.amazonaws.com/rstudio-ide-build/server/${RSW_OS}/${RSW_ARCH}/${RSW_NAME}-${RSW_VERSION}-${RSW_ARCH}.deb

RUN curl -o rstudio-workbench.deb ${RSW_DOWNLOAD_URL}

RUN apt-get update -y && \
    gdebi rstudio-workbench.deb
	
RUN rm rstudio-workbench.deb && \
	rm -rf /var/lib/rstudio-server/r-versions
	
EXPOSE 8788/tcp	
