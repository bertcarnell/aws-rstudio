FROM ubuntu-rstudio-3-java

RUN apt-get update -y && \
    apt-get install -y gpg

# https://cran.r-project.org/bin/linux/ubuntu/fullREADME.html
RUN echo "deb https://cran.microsoft.com/bin/linux/ubuntu jammy-cran40/" >> /etc/apt/sources.list

RUN wget -qO- https://cran.microsoft.com/bin/linux/ubuntu/marutter_pubkey.asc | tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc

RUN gpg --show-keys /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc

RUN apt-get update -y && \
    apt-get install -y \
	r-base \
	r-base-dev \
	r-recommended


