FROM ubuntu:14.04

WORKDIR /root
USER root

# System Packages
RUN apt-get update
RUN apt-get -y install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev python-software-properties libffi-dev
RUN apt-get -y install libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev wget

# Install Elasticsearch
RUN apt-get -y install openjdk-7-jre-headless
RUN wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.5.0.deb
RUN dpkg -i elasticsearch-1.5.0.deb

# Install Wrapper for Elasticsearch
RUN curl -L http://github.com/elasticsearch/elasticsearch-servicewrapper/tarball/master | tar -xz
RUN mkdir /usr/local/share/elasticsearch
RUN mkdir /usr/local/share/elasticsearch/bin
RUN mv *servicewrapper*/service /usr/local/share/elasticsearch/bin/
RUN rm -Rf *servicewrapper*

# Install rbenv
RUN git clone https://github.com/sstephenson/rbenv.git /usr/local/rbenv
RUN echo '# rbenv setup' > /etc/profile.d/rbenv.sh
RUN echo 'export RBENV_ROOT=/usr/local/rbenv' >> /etc/profile.d/rbenv.sh
RUN echo 'export PATH="$RBENV_ROOT/bin:$PATH"' >> /etc/profile.d/rbenv.sh
RUN echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh
RUN chmod +x /etc/profile.d/rbenv.sh

# Install ruby-build
RUN mkdir /usr/local/rbenv/plugins
RUN git clone https://github.com/sstephenson/ruby-build.git /usr/local/rbenv/plugins/ruby-build

# Install ruby 2.2.1
ENV PATH /usr/local/rbenv/shims:/usr/local/rbenv/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV RBENV_ROOT /usr/local/rbenv
RUN rbenv install 2.2.1
