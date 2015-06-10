# Taken from https://freeswitch.org/confluence/display/FREESWITCH/Debian#Debian-DebianPackage

FROM debian:wheezy
MAINTAINER Praekelt Foundation <dev@praekeltfoundation.org>

# Add the repository
RUN echo 'deb http://files.freeswitch.org/repo/deb/debian/ wheezy main' \
    >> /etc/apt/sources.list.d/freeswitch.list
RUN gpg --keyserver pool.sks-keyservers.net --recv-key D76EDC7725E010CF
RUN gpg -a --export D76EDC7725E010CF | apt-key add -

# Install the packages
RUN apt-get update
ADD retry_until_pass.sh .
RUN ./retry_until_pass.sh apt-get install -y freeswitch-meta-vanilla

# Copy configuration files
RUN cp -a /usr/share/freeswitch/conf/vanilla /etc/freeswitch
WORKDIR /etc/freeswitch

# Run freeswitch
EXPOSE 8021
CMD /usr/bin/freeswitch -c