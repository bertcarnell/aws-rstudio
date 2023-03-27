FROM ubuntu-rstudio-5-rpackages

ARG CONDA_PYTHON_VERSION=3.9.5
ARG DRIVERS_VERSION=2022.11.0_amd64
ARG SNOWFLAKE_ODBC_VERSION=2.25.10

# Install Python -------------------------------------------------------------#

#RUN apt-get update -y && \
#    apt-get install -y python3 python3-pip
#
#RUN python3 --version

RUN curl -O https://repo.anaconda.com/miniconda/Miniconda3-4.7.12.1-Linux-x86_64.sh && \
    bash Miniconda3-4.7.12.1-Linux-x86_64.sh -bp /opt/python/${CONDA_PYTHON_VERSION} && \
    /opt/python/${CONDA_PYTHON_VERSION}/bin/conda install -y python==${CONDA_PYTHON_VERSION} && \
    rm -rf Miniconda3-*-Linux-x86_64.sh

ENV PATH="/opt/python/${CONDA_PYTHON_VERSION}/bin:${PATH}"

# Install RStudio Professional Drivers ---------------------------------------#
# docs.posit.co/pro-drivers/workbench-connect

RUN apt-get update -y && \
    apt-get install -y unixodbc unixodbc-dev gdebi libaio1 libsasl2-dev

RUN curl -O https://drivers.rstudio.org/7C152C12/installer/rstudio-drivers_${DRIVERS_VERSION}.deb && \
    gdebi rstudio-drivers_${DRIVERS_VERSION}.deb && \
    rm -f rstudio-drivers_${DRIVERS_VERSION}.deb && \
    cp /etc/odbcinst.ini /etc/odbcinst.ini.bak && \
	cat /opt/rstudio-drivers/odbcinst.ini.sample | tee -a /etc/odbcinst.ini

# r-cran-odbc not built for ubuntu
RUN Rscript -e 'install.packages("odbc", repos="https://cran.microsoft.com")'

# RStudio-specific customizations --------------------------------------------#

RUN apt-get update -y && \
    apt-get install -y \
	r-cran-reticulate \
	r-cran-readr \
	r-cran-curl \
	r-cran-ggplot2 \
	r-cran-dplyr \
	r-cran-stringr \
	r-cran-remotes \
	r-cran-urca \
	r-cran-sodium \
	r-cran-plumber \
	r-cran-jsonlite

# r-cran-odbc not built for ubuntu
RUN Rscript -e 'install.packages(c("fable", "tsibble", "feasts"), repos="https://cran.microsoft.com")'
	
RUN /opt/python/${CONDA_PYTHON_VERSION}/bin/pip install --upgrade \
        'boto3>1.0<2.0' \
        'awscli>1.0<2.0' \
        'sagemaker[local]<3' \
        'sagemaker-studio-image-build' \
        'numpy'

# Locale configuration -------------------------------------------------------#

RUN apt-get update -y && \
    apt-get install -y libc6  libc6-dev locales

RUN localedef -i en_US -f UTF-8 en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Studio-specific customizations ---------------------------------------------#

RUN apt-get update -y && \
    apt-get install -y sudo \
    vim \
    openjdk-11-jdk \
    libpng-dev

# Set default env values
# RSessionGateway consumes these environment variables to do dynamic configuration in rsession.conf.
ENV RSTUDIO_CONNECT_URL ""
ENV RSTUDIO_PACKAGE_MANAGER_URL ""

# Snowflake ------------------------------------------------------------------#
# developers.snowflake.com/odbc

RUN curl -O https://sfc-repo.snowflakecomputing.com/odbc/linux/${SNOWFLAKE_ODBC_VERSION}/snowflake-odbc-${SNOWFLAKE_ODBC_VERSION}.x86_64.deb && \
    dpkg -i snowflake-odbc-${SNOWFLAKE_ODBC_VERSION}.x86_64.deb

# AWS CLI 2 ------------------------------------------------------------------#
# docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
	./aws/install
	





