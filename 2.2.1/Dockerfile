FROM ubuntu:14.04

# User ubuntu (does not work with current docker)
RUN apt-get update
RUN apt-get -y install sudo
# RUN useradd ubuntu && echo "ubuntu:ubuntu" | chpasswd && adduser ubuntu sudo
# RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
# RUN mkdir -p /home/ubuntu && chown -R ubuntu:ubuntu /home/ubuntu
# USER ubuntu
# CMD /bin/bash
# WORKDIR /home/ubuntu

# System Packages
RUN sudo apt-get -y install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev python-software-properties libffi-dev
RUN sudo apt-get -y install libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev wget
RUN sudo apt-get -y install libmysqlclient-dev nodejs mysql-client-5.6

# Install Elasticsearch
RUN sudo apt-get -y install openjdk-7-jre-headless
RUN wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.5.0.deb
RUN sudo dpkg -i elasticsearch-1.5.0.deb
RUN mkdir /usr/share/elasticsearch/config
RUN cp /etc/elasticsearch/elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml
RUN cp /etc/elasticsearch/logging.yml /usr/share/elasticsearch/config/logging.yml

# Install Wrapper for Elasticsearch
# RUN curl -L http://github.com/elasticsearch/elasticsearch-servicewrapper/tarball/master | tar -xz
# RUN sudo mkdir /usr/local/share/elasticsearch
# RUN sudo mkdir /usr/local/share/elasticsearch/bin
# RUN sudo mv *servicewrapper*/service /usr/local/share/elasticsearch/bin/
# RUN rm -Rf *servicewrapper*

# Install rbenv
RUN git clone https://github.com/sstephenson/rbenv.git /usr/local/rbenv
RUN git clone https://github.com/sstephenson/ruby-build.git /usr/local/rbenv/plugins/ruby-build
ADD rbenv.sh /etc/drone.d/
ADD rbenv.sh /etc/profile.d/
ENV PATH /usr/local/rbenv/shims:/usr/local/rbenv/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV RBENV_ROOT /usr/local/rbenv
RUN eval "$(rbenv init -)"

# Install ruby 2.2.1
ENV CONFIGURE_OPTS --disable-install-doc
RUN rbenv install 2.2.1
RUN rbenv global 2.2.1
RUN rbenv rehash

# Bundler
RUN echo 'gem: --no-rdoc --no-ri' >> .gemrc
RUN gem install rbenv-rehash
RUN gem install bundler
RUN rbenv rehash
