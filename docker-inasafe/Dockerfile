#--------- Generic stuff all our Dockerfiles should start with so we get caching ------------
FROM inasafe/qgis-desktop:2.4
MAINTAINER Akbar Gumbira <akbargumbira@gmail.com>

RUN export DEBIAN_FRONTEND=noninteractive
ENV DEBIAN_FRONTEND noninteractive
RUN dpkg-divert --local --rename --add /sbin/initctl

# Use local cached debs from host (saves your bandwidth!)
# Change ip below to that of your apt-cacher-ng host
# Or comment this line out if you do not wish to use caching
ADD 71-apt-cacher-ng /etc/apt/apt.conf.d/71-apt-cacher-ng

RUN echo "deb http://archive.ubuntu.com/ubuntu trusty main universe" > /etc/apt/sources.list
RUN apt-get -y update
RUN apt-get -y install rpl pwgen git

#-------------Application Specific Stuff ----------------------------------------------------
# Install QGIS 2.4, git, xvfb
RUN apt-get -y install git xvfb
# Called on first run of docker - will run make-latest-shakemap.sh
ADD start.sh /start.sh
RUN chmod 0755 /start.sh

CMD /start.sh
