############################################################
# Dockerfile for a Ubuntu-dev container image
# Based on Ubuntu
############################################################

# Set the base image to Ubuntu
FROM ubuntu:15.10

# File Author / Maintainer
MAINTAINER anders.roxell@linaro.org

# Make sure apt-get isn't interactive
ENV DEBIAN_FRONTEND noninteractive

# Update database and install base packages
RUN apt-get update && apt-get install -y --no-install-recommends \
	# Base packages
	build-essential \
	ca-certificates \
	curl \
	gcc-multilib \
	git-core \
	inetutils-ping \
	inetutils-tools \
	libc6-dev-i386 \
	lib32stdc++6 \
	lib32z1 \
	net-tools \
	wget \
	# Extra
	sshfs \
	# Cleanup
	&& apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# bin-directory for scripts
RUN mkdir -p /root/bin
ENV PATH /root/bin:$PATH

ADD mountsshfs /root/bin/mountsshfs

ENV HOSTNAME ubuntu-dev-1510

ENTRYPOINT /bin/bash
