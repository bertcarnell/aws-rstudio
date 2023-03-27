FROM aws-rstudio-1-system

ARG RSW_VERSION=2022.02.2+485.pro2
ARG RSW_NAME=rstudio-workbench-rhel
ARG RSW_DOWNLOAD_URL=https://s3.amazonaws.com/rstudio-ide-build/server/centos7/x86_64

RUN RSW_VERSION_URL=`echo -n "${RSW_VERSION}" | sed 's/+/-/g'` && \
    curl -o rstudio-workbench.rpm ${RSW_DOWNLOAD_URL}/${RSW_NAME}-${RSW_VERSION_URL}-x86_64.rpm 

RUN ls -alh

RUN yum update -y && \
    yum install -y rstudio-workbench.rpm && \
	yum clean all
	
RUN rm rstudio-workbench.rpm && \
	rm -rf /var/lib/rstudio-server/r-versions
	
EXPOSE 8788/tcp	
