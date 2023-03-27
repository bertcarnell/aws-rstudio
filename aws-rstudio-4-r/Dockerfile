FROM aws-rstudio-3-java

ARG R_VERSION=4.2.2
ARG SQLITE_VERSION=3410200
ARG CMAKE_VERSION=3.25.3
ARG PROJ_VERSION=9.2.0
ARG GDAL_VERSION=3.6.3
ARG GEOS_VERSION=3.11.2

RUN yum update -y && \
    yum install -y \
	libxml2-devel \
	make \
	automake \
	gcc \
	gcc-c++ \
	libcurl-devel \
	libtiff \
	libtiff-devel \
	bzip2 \
	udunits2-devel
	
RUN cd /tmp && \
    curl -L https://sqlite.org/2023/sqlite-autoconf-${SQLITE_VERSION}.tar.gz | tar zxf - && \
	curl -L https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}.tar.gz | tar zxf - && \
	curl -L https://download.osgeo.org/proj/proj-${PROJ_VERSION}.tar.gz | tar zxf - && \
	curl -L https://github.com/OSGeo/gdal/releases/download/v${GDAL_VERSION}/gdal-${GDAL_VERSION}.tar.gz | tar zxf - && \
	curl -L https://download.osgeo.org/geos/geos-${GEOS_VERSION}.tar.bz2 | tar jxf -

RUN cd /tmp/sqlite-autoconf-${SQLITE_VERSION} && \
    ./configure --enable-rtree && \
	make && \
	make install
	
RUN cd /tmp/cmake-${CMAKE_VERSION} && \
    ./bootstrap && \
	make && \
	make install

RUN cd /tmp/proj-${PROJ_VERSION} && \
    mkdir build && \
	cd build && \
	cmake -DBUILD_TESTING=False .. && \
	cmake --build . --target install

RUN cd /tmp/gdal-${GDAL_VERSION} && \
    mkdir build && \
	cd build && \
	cmake -DBUILD_TESTING=False -DACCEPT_MISSING_SQLITE3_RTREE=ON .. && \
	cmake --build . && \
	cmake --build . --target install
	
RUN cd /tmp/geos-${GEOS_VERSION} && \
    mkdir build && \
	cd build && \
	cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=False -DBUILD_DOCUMENTATION=OFF .. && \
	make && \
	make install
	
RUN curl -O https://cdn.rstudio.com/r/centos-7/pkgs/R-${R_VERSION}-1-1.x86_64.rpm && \
    yum install -y R-${R_VERSION}-1-1.x86_64.rpm && \
	yum clean all && \
	rm -rf R-${R_VERSION}-1-1.x86_64.rpm

RUN ln -s /opt/R/${R_VERSION}/bin/R /usr/local/bin/R && \
    ln -s /opt/R/${R_VERSION}/bin/Rscript /usr/local/bin/Rscript
	
# ensure that the /opt/R/${R_VERSION}/lib/R/etc/ldpaths file is correct for the installed java
RUN /opt/R/${R_VERSION}/bin/R CMD javareconf

RUN echo -e "Path: /opt/R/${R_VERSION}\nLabel: R Version with test rJava and rgdal\nScript: /opt/R/${R_VERSION}/lib/R/etc/ldpaths\nRepo: https://cran.microsoft.com/" >> /etc/rstudio/r-versions


