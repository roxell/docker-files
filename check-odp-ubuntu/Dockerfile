############################################################
# Dockerfile to build check-odp container images
# Based on Ubuntu
############################################################

# Set the base image to Ubuntu
FROM roxell/ubuntu-dev:15.04

# File Author / Maintainer
MAINTAINER anders.roxell@linaro.org

# Make sure apt-get isn't interactive
ENV DEBIAN_FRONTEND noninteractive

# Update database and install base packages
RUN apt-get update && apt-get install -y --no-install-recommends \
	# ODP deps
	autoconf \
	automake \
	asciidoc \
	libcunit1-dev \
	doxygen \
	graphviz \
	ifupdown \
	imagemagick \
	lcov \
	librsvg2-bin \
	libssl-dev \
	libtool \
	source-highlight \
	texlive-latex-recommended \
	# ODP optional deps
	clang \
	# Smatch deps
	libsqlite3-dev \
	# DPDK deps
	linux-headers-3.19.0-30-generic \
	linux-image-3.19.0-30-generic \
	libpcap-dev \
	sudo \
	# Cleanup
	&& apt-get remove -y \
	texlive-latex-recommended-doc \
	texlive-latex-base-doc \
	texlive-pictures-doc \
	texlive-pstricks-doc \
	&& apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN git config --global user.name "Docker ODP" \
	&& git config --global user.email docker_odp@linaro.org \
	&& git config --global color.ui auto

# Smatch
RUN cd && git clone git://repo.or.cz/smatch.git \
	&& cd smatch && make PREFIX=/usr install && git clean -xdf \
	&& cd - && rm -rf $HOME/smatch

# Sparse
RUN cd && git clone -b v0.5.0 git://git.kernel.org/pub/scm/devel/sparse/sparse.git \
	&& cd sparse && make PREFIX=/usr install && git clean -xdf \
	&& cd - && rm -rf $HOME/sparse

# Needed for check-odp
ADD check-odp /root/bin/check-odp

# Needed to build DPDK
ADD uname /root/bin/uname

ENV HOSTNAME odp-ubuntu-1504
