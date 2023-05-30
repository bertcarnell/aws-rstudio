FROM ubuntu-sms-6

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

RUN apt-get update && \
    apt-get install -y sudo && \
	chmod g+w /etc/passwd && \
	echo "${NB_USER}    ALL=(ALL)    NOPASSWD:    ALL" >> /etc/sudoers && \
	rm -rf /var/lib/apt/lists/*

# RScript to get the user space created
RUN Rscript -e 'dir.create(Sys.getenv("R_LIBS_USER"), recursive = TRUE)'

RUN Rscript -e '.libPaths()'

RUN fix-permissions /home/sagemaker-user

WORKDIR $HOME
USER ${NB_UID}
