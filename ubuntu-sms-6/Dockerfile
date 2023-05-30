FROM ubuntu-sms-5

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
	r-cran-cli \
	r-cran-glue \
	r-cran-bit \
	r-cran-vctrs \
	r-cran-lifecycle \
	r-cran-pkgconfig \
	r-cran-bit64 \
	r-cran-blob \
	r-cran-dbi \
	r-cran-hms \
	r-cran-rcpp \
	r-cran-rlang
	
	
RUN apt-get update --fix-missing && \
    apt-get upgrade -yq && \
	apt-get install -yq --no-install-recommends \
    r-cran-argparse \
	r-cran-bslib \
	r-cran-car \
	r-cran-caret \
	r-cran-cli \
	r-cran-crayon \
	r-cran-curl \
	r-cran-data.table \
	r-cran-dbplyr \
	r-cran-distributional \
	r-cran-devtools \
	r-cran-doparallel \
	r-cran-dplyr \
	r-cran-dtplyr \
	r-cran-forcats \
	r-cran-foreach \
	r-cran-forecast \
	r-cran-formula \
	r-cran-futile.logger \
	r-cran-ggplot2 \
	r-cran-ggridges \
	r-cran-gplots \
	r-cran-gridextra \
	r-cran-haven \
	r-cran-hexbin \
	r-cran-hmisc \
	r-cran-htmltools \
	r-cran-htmlwidgets \
	r-cran-httr \
	r-cran-irdisplay \
	r-cran-iterators \
	r-cran-jsonlite \
	r-cran-jquerylib \
	r-cran-keyring \
	r-cran-knitr \
	r-cran-knitr \
	r-cran-lme4 \
	r-cran-logger \
	r-cran-lubridate \
	r-cran-markdown \
	r-cran-nloptr \
	r-cran-openxlsx \
	r-cran-pbdzmq \
	r-cran-plotly \
	r-cran-plumber \
	r-cran-plyr \
	r-cran-proto \
	r-cran-pwr \
	r-cran-randomforest \
	r-cran-rcurl \
	r-cran-readr \
	r-cran-readxl \
	r-cran-remotes \
	r-cran-remotes \
	r-cran-repr \
	r-cran-reprex \
	r-cran-reticulate \
	r-cran-rgdal \
	r-cran-rjava \
	r-cran-rmarkdown \
	r-cran-rocr \
	r-cran-rodbc \
	r-cran-r.methodss3 \
	r-cran-r.oo \
	r-cran-rstan \
	r-cran-rstanarm \
	r-cran-rstantools \
	r-cran-r.utils \
	r-cran-rvest \
	r-cran-scales \
	r-cran-sendmailr \
	r-cran-sf \
	r-cran-shiny \
	r-cran-sqldf \
	r-cran-slider \
	r-cran-sodium \
	r-cran-sp \
	r-cran-stringi \
	r-cran-stringr \
	r-cran-tibble \
	r-cran-tidyr \
	r-cran-urca \
	r-cran-uuid \
	r-cran-warp \
	r-cran-webshot2

RUN apt-get update --fix-missing && \
    apt-get upgrade -yq && \
	apt-get install -yq --no-install-recommends \
	r-cran-anytime \
	r-cran-aws.s3 \
	r-cran-aws.lambda \
	r-cran-azureauth \
	r-cran-azuregraph \
	r-cran-blastula \
	r-cran-botor \
	r-cran-config \
	r-cran-feasts \
	r-cran-feather \
	r-cran-fable \
	r-cran-fabletools \
	r-cran-financialmath \
	r-cran-fincal \
	r-cran-flexdashboard \
	r-cran-forge \
	r-cran-getpass \
	r-cran-ggcorrplot \
	r-cran-jose \
	r-cran-mailr \
	r-cran-microsoft365r \
	r-cran-piton \
	r-cran-r2d3 \
	r-cran-rathena \ 
	r-cran-rgeos \
	r-cran-rjdbc \
	r-cran-skimr \
	r-cran-sparklyr \
	r-cran-tidyxl \
	r-cran-tsibble \
	r-cran-xgboost

RUN apt-get install -yqf --no-install-recommends && \
    apt-get autoremove && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*
	

WORKDIR $HOME
USER ${NB_UID}


	