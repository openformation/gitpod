FROM ubuntu:20.04

LABEL authors="André König <andre.koenig@openformation.io>"

ARG DEBIAN_FRONTEND=noninteractive

#
# Version Configuration
#
ARG GCLOUD_SDK_VERSION=384.0.1
ARG GITHUB_CLI_VERSION=2.6.0

#
# Install base dependencies
#
RUN apt update
RUN apt install -yq --no-install-recommends \
      sudo \
      curl \
      tig \
      gnupg \
      tzdata \
      ca-certificates \
      software-properties-common \
      vim \
      zsh

#
# Gitpod User (from Gitpod base Dockerfile)
#
# '-l': see https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#user
RUN useradd -l -u 33333 -G sudo -md /home/gitpod -s /bin/bash -p gitpod gitpod \
    # passwordless sudo for users in the 'sudo' group
    && sed -i.bkp -e 's/%sudo\s\+ALL=(ALL\(:ALL\)\?)\s\+ALL/%sudo ALL=NOPASSWD:ALL/g' /etc/sudoers
ENV HOME=/home/gitpod

WORKDIR $HOME

USER gitpod
# use sudo so that user does not get sudo usage info on (the first) login
RUN sudo echo "Running 'sudo' for Gitpod: success" && \
    # create .bashrc.d folder and source it in the bashrc
    mkdir -p /home/gitpod/.bashrc.d && \
    (echo; echo "for i in \$(ls -A \$HOME/.bashrc.d/); do source \$HOME/.bashrc.d/\$i; done"; echo) >> /home/gitpod/.bashrc

# custom Bash prompt
RUN { echo && echo "PS1='\[\033[01;32m\]\u\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\] $ '" ; } >> .bashrc.d/bash-prompt

#
# Google Cloud SDK Installation Preparation
#
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -

ENV CLOUDSDK_PYTHON=python3

#
# GitHub CLI Installation Preparation
#
RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg && \
  echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null

#
# Docker
#
# IMPORTANT: We're installing for `focal` here (as there is not candidate for Ubuntu 22.04 right now)
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && \
  sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

RUN sudo curl -o /usr/bin/slirp4netns -fsSL https://github.com/rootless-containers/slirp4netns/releases/download/v1.1.12/slirp4netns-$(uname -m) \
    && sudo chmod +x /usr/bin/slirp4netns

RUN sudo curl -o /usr/local/bin/docker-compose -fsSL https://github.com/docker/compose/releases/download/1.29.2/docker-compose-Linux-x86_64 \
    && sudo chmod +x /usr/local/bin/docker-compose

#
# Installation
#
RUN sudo apt update && \
    sudo apt install -yq \
    docker-ce \
    docker-ce-cli \
    containerd.io \
    locales && \
    sudo apt dist-upgrade -y

#
# Install dedicated versions of tools AFTER
# ̀AFTER `dist-upgrade`
#
RUN sudo apt install -yq \
    gh=$GITHUB_CLI_VERSION \
    google-cloud-sdk=$GCLOUD_SDK_VERSION-0

#
# Correct Character Encoding
#
RUN sudo sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen && sudo locale-gen
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8 

#
# Cleanup
#
RUN sudo apt-get clean -yq && \
  sudo rm -rf \
   /var/cache/debconf/* \
   /var/lib/apt/lists/* \
   /tmp/* \
   /var/tmp/*
