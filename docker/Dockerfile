FROM ubuntu

LABEL version="0.5"
LABEL date="17-12-2022"
LABEL author="fernando.pacheco@s4g.es; victor.bereciartu@s4g.es"

## To fix "debconf: delaying package configuration, since apt-utils is not installed"
ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NOWARNINGS="yes"
## Set TERM to select console colors
ENV TERM xterm-256color
## Set encoding to avoid problems with spanish characters
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

## Update system
RUN apt-get update
## Encoding
RUN apt-get -y install locales
RUN locale-gen en_US.UTF-8
## Java
RUN echo y | apt-get install default-jdk
## Git
RUN echo y | apt-get install git
## Manage JSON files
RUN echo y | apt-get install jq
## Tools to get packages to install
RUN apt-get install wget
RUN echo y | apt-get install curl
## Node
RUN curl -fsSL https://deb.nodesource.com/setup_19.x | bash -
RUN apt-get install -y nodejs
## Salesforce SFDX
RUN npm install sfdx-cli --location=global
## SFDX plugins
RUN echo y | sfdx plugins:install sfdx-git-delta
RUN sfdx plugins
## Local date hour
RUN echo 'tzdata tzdata/Areas select Europe' | debconf-set-selections
RUN echo 'tzdata tzdata/Zones/Europe select Madrid' | debconf-set-selections
RUN apt-get install -y tzdata

## Copy git config in work directory
COPY config/.gitconfig /root
## Copy ssh config
RUN mkdir /root/.ssh
COPY config/.ssh /root/.ssh

## When the container is running this command allows it to live as long as there are executions
CMD ["/bin/bash"]