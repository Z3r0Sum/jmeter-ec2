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
ENV JMETER_VERSION 2.13 
ENV JMETER_HOME="/var/lib/apache-jmeter-${JMETER_VERSION}"
ENV PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
# Heap size for either the client or server in MB
ENV JM_HEAP=1024

COPY dependencies /tmp/dependencies

# Install the JDK
RUN dnf install -y java-$JDK_VERSION-openjdk-devel.x86_64 && rm -rf /var/cache/yum && \
  dnf install -y tar \
  && dnf install -y bzip2 dbus-glib gtk2 libXt unzip \
  && curl -O https://ftp.mozilla.org/pub/firefox/releases/26.0/linux-x86_64/en-US/firefox-26.0.tar.bz2 \
  && bzip2 -d firefox-26.0.tar.bz2 \
  && tar xf firefox-26.0.tar \
  && export PATH=$PATH:/firefox 

COPY dependencies/apache-jmeter-$JMETER_VERSION.tgz /var/lib/

# Install JMeter
RUN cd /var/lib \
  && /usr/bin/tar xvfz apache-jmeter-$JMETER_VERSION.tgz \
  && unzip -oq "/tmp/dependencies/JMeterPlugins-*.zip" -d $JMETER_HOME \
  && rm -rf /tmp/dependencies \
  && rm -f /var/lib/apache-jmeter-$JMETER_VERSION/lib/http*-4.5.jar \ 
  && rm -f /var/lib/apache-jmeter-$JMETER_VERSION/lib/httpcore-4.4.1.jar

COPY scripts/jmeter /var/lib/apache-jmeter-$JMETER_VERSION/bin/
