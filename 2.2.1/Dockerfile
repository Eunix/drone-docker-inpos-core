FROM bradrydzewski/base

USER root
WORKDIR /root

# System Packages
RUN apt-get -y install libmysqlclient-dev nodejs

# Install Elasticsearch
RUN apt-get -y install openjdk-7-jre-headless
RUN wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.5.0.deb
RUN dpkg -i elasticsearch-1.5.0.deb
RUN mkdir /usr/share/elasticsearch/config
RUN cp /etc/elasticsearch/elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml
RUN cp /etc/elasticsearch/logging.yml /usr/share/elasticsearch/config/logging.yml

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
