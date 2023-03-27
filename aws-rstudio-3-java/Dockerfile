FROM aws-rstudio-2-rstudio

RUN yum update -y && \
    yum install -y java-1.8.0-openjdk-devel
	
RUN java -version

RUN ls /usr/lib/jvm

ENV JAVA_HOME /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.362.b08-1.amzn2.0.1.x86_64

