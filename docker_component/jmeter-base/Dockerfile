#
# Dockerfile for a base jmeter image
# 
# Usage:
# It is unlikely that you will need to run this image.
# It forms the basis for other images.
#

FROM fedora
MAINTAINER Sri Sankaran sri@redhat.com

# Describe the environment
ENV JDK_VERSION 1.8.0
ENV JMETER_VERSION 3.0

# Install the JDK
RUN dnf install -y java-$JDK_VERSION-openjdk-devel.x86_64 && rm -rf /var/cache/yum && \
  dnf install -y tar

COPY apache-jmeter-3.0.tgz /var/lib

# Install JMeter
RUN cd /var/lib \
  && /usr/bin/tar xvfz apache-jmeter-3.0.tgz
