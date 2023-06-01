#------------- https://github.com/aws-samples/sagemaker-studio-custom-image-samples/blob/main/examples/r-image/Dockerfile ----------

# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
#ARG OWNER=jupyter
#ARG BASE_CONTAINER=$OWNER/minimal-notebook
FROM ubuntu-sms-3

LABEL maintainer="Jupyter Project <jupyter@googlegroups.com>"

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

# R pre-requisites
#RUN apt-get update --yes && \
#    apt-get install --yes --no-install-recommends \
#    fonts-dejavu \
#    unixodbc \
#    unixodbc-dev \
#    r-cran-rodbc \
#    gfortran \
#    gcc && \
#    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN apt-get update --yes && \
    apt-get install --yes --no-install-recommends \
    fonts-dejavu \
    unixodbc \
    unixodbc-dev \
    gfortran \
    gcc && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
	
# install R
## Step 1

RUN apt update -qq && apt install --yes --no-install-recommends wget \
    ca-certificates gnupg && \
    wget -q -O- https://eddelbuettel.github.io/r2u/assets/dirk_eddelbuettel_key.asc \
    | tee -a /etc/apt/trusted.gpg.d/cranapt_key.asc
	
## Step 2

RUN echo "deb [arch=amd64] https://r2u.stat.illinois.edu/ubuntu jammy main" \
    > /etc/apt/sources.list.d/cranapt.list && \
    apt update -qq
	
## Step 3

RUN wget -q -O- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc \
    | tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc && \
    echo "deb [arch=amd64] https://cloud.r-project.org/bin/linux/ubuntu jammy-cran40/" \
    > /etc/apt/sources.list.d/cran_r.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys \
    67C2D66C4B1D4339 51716619E084DAB9 && \
    apt update -qq && \
    DEBIAN_FRONTEND=noninteractive apt install --yes --no-install-recommends \
    r-base-core \
	r-base \
	r-base-dev \
	r-recommended
	
## Step 4

USER root

RUN echo "Package: *" > /etc/apt/preferences.d/99cranapt && \
    echo "Pin: release o=CRAN-Apt Project" >> /etc/apt/preferences.d/99cranapt && \
    echo "Pin: release l=CRAN-Apt Packages" >> /etc/apt/preferences.d/99cranapt && \
    echo "Pin-Priority: 700"  >> /etc/apt/preferences.d/99cranapt
    
# R packages including IRKernel which gets installed globally.
# r-e1071: dependency of the caret R package
#RUN mamba install --quiet --yes \
#    'r-base' \
#    'r-caret' \
#    'r-crayon' \
#    'r-devtools' \
#    'r-e1071' \
#    'r-forecast' \
#    'r-hexbin' \
#    'r-htmltools' \
#    'r-htmlwidgets' \
#    'r-irkernel' \
#    'r-nycflights13' \
#    'r-randomforest' \
#    'r-rcurl' \
#    'r-reticulate' \
#    'r-rmarkdown' \
#    'r-rodbc' \
#    'r-rsqlite' \
#    'r-shiny' \
#    'r-tidyverse' \
#    'boto3' \
#    'sagemaker' \
#    'unixodbc' && \
#    mamba clean --all -f -y && \
#    fix-permissions "${CONDA_DIR}" && \
#    fix-permissions "/home/${NB_USER}"

RUN mamba install --quiet --yes \
    'boto3' \
	'awscli' \
    'sagemaker' \
    'unixodbc' \
	'sagemaker-studio-image-build' \
	'numpy' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# `r-tidymodels` is not easy to install under arm
#RUN set -x && \
#    arch=$(uname -m) && \
#    if [ "${arch}" == "x86_64" ]; then \
#        mamba install --quiet --yes \
#            'r-tidymodels' && \
#            mamba clean --all -f -y && \
#            fix-permissions "${CONDA_DIR}" && \
#            fix-permissions "/home/${NB_USER}"; \
#    fi;

RUN apt-get update -y && \
    apt-get install -y r-cran-irkernel
	
RUN Rscript -e 'IRkernel::installspec(user = FALSE)'

RUN useradd --non-unique --create-home --shell /bin/bash --gid "${NB_GID}" --uid ${NB_UID} "sagemaker-user"
    
WORKDIR $HOME
USER ${NB_UID}
