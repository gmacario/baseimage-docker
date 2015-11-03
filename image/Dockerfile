FROM ubuntu:14.04
MAINTAINER Gianpaolo Macario <gmacario@gmail.com>

# Create mountpoint for Vagrant synced folder
RUN mkdir -p /vagrant

ADD . /bd_build

# Create user "vagrant"
RUN apt-get update && apt-get -y install adduser
RUN adduser vagrant
# Change default password for user "vagrant"
RUN usermod -p $(perl -e 'print crypt("vagrant","\$6\$xx\$")') vagrant
# Allow user "vagrant" to become root without entering a password
RUN install -m 440 /bd_build/etc_sudoers.d_vagrant /etc/sudoers.d/vagrant

# Create mountpoint for Vagrant synced folder
RUN mkdir -p /vagrant

RUN /bd_build/prepare.sh && \
	/bd_build/system_services.sh && \
	/bd_build/utilities.sh && \
	/bd_build/cleanup.sh

CMD ["/sbin/my_init"]
