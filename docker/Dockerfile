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
        python-is-python3 \
        python3 \
        python3-pip \
        rsync \
        unzip \
        vim \
        wget \
        zip \
    && rm -rf /var/lib/apt/lists/*

# copy the repo source (e.g. notebooks) to the container image
ARG ML101_HASH="de82d6c5221d79a3358f16c3441ebfc9147f6dfa"
RUN git clone https://github.com/nesi/sklearn_tutorial.git /opt/sklearn_tutorial \
    && cd /opt/sklearn_tutorial \
    && git checkout $ML101_HASH \
    && rm -rf /opt/sklearn_tutorial/.git

# copy requirements.txt and install dependencies
COPY requirements.txt /opt/sklearn_tutorial/
RUN pip3 --no-cache-dir install -r requirements.txt \
    && pip3 --no-cache-dir install jupyterlab \

# copy cleanup script
COPY cleanup-homes /usr/local/bin/
