FROM ubuntu:22.04

# install system dependencies
# TODO: move ldap-utils, libnss-ldapd, libpam-ldapd, nscd, nslcd to base image??
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        curl \
        git \
        ldap-utils \
        libnss-ldapd \
        libpam-ldapd \
        less \
        nano \
        nodejs \
        nscd \
        nslcd \
        rsync \
        unzip \
        vim \
        wget \
        zip \
    && rm -rf /var/lib/apt/lists/*

# install miniconda
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /miniconda.sh \
    && bash /miniconda.sh -b -p /opt/miniconda3 \
    && rm -f /miniconda.sh

# copy the repo source (e.g. notebooks) to the container image
ARG ML101_HASH="dfb7a172a49f76f7c0ab1f9a96fa9b92aafaac96"
RUN git clone https://github.com/nesi/sklearn_tutorial.git /opt/sklearn_tutorial \
    && cd /opt/sklearn_tutorial \
    && git checkout $ML101_HASH \
    && rm -rf /opt/sklearn_tutorial/.git \
    && . /opt/miniconda3/etc/profile.d/conda.sh \
    && conda config --set auto_activate_base false \
    && conda env create -f /opt/sklearn_tutorial/environment.yml -p /var/lib/skl_tut \
    && echo ". /opt/miniconda3/etc/profile.d/conda.sh" > /etc/profile.d/conda.sh \
    && echo "conda activate /var/lib/skl_tut" >> /etc/profile.d/conda.sh \
    && conda clean -afy
