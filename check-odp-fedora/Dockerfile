############################################################
# Dockerfile to build check-odp container images
# Based on Fedora
############################################################

# Set the base image to Fedora
FROM fedora:22

# File Author / Maintainer
MAINTAINER anders.roxell@linaro.org

# Update database and install base packages
RUN dnf -y update && dnf install -y \
	# Base packages
	gcc \
	gcc-c++ \
	glibc-devel.x86_64 \
	libstdc++.i686 \
	libstdc++-devel.i686 \
	glibc.i686 \
	glibc-devel.i686 \
	zlib.i686 \
	zlib-devel.i686 \
	make \
	graphviz \
	git \
	curl \
	wget \
	bzip2 \
	iproute \
	# ODP deps
	autoconf \
	automake \
	libtool \
	doxygen \
	openssl-devel \
	# ODP optional deps
	clang \
	# Smatch deps
	sqlite-devel \
	# DPDK deps
	kernel-headers \
	kernel-modules \
	libpcap-devel \
	# Extra
	sshfs \
	# Cleanup
	&& dnf clean all

RUN git config --global user.name "Docker ODP" \
	&& git config --global user.email docker_odp@linaro.org \
	&& git config --global color.ui auto

RUN cd && git clone git://repo.or.cz/smatch.git \
	&& cd smatch && make PREFIX=/usr install && git clean -xdf \
	&& cd - && rm -rf $HOME/smatch

# Sparse
RUN cd && git clone -b v0.5.0 git://git.kernel.org/pub/scm/devel/sparse/sparse.git \
	&& cd sparse && make PREFIX=/usr install && git clean -xdf \
	&& cd - && rm -rf $HOME/sparse

# bin-directory for scripts
RUN mkdir -p /root/bin
ENV PATH /root/bin:$PATH

# Needed for check-odp
ADD mountsshfs /root/bin/mountsshfs
ADD check-odp /root/bin/check-odp

# Needed to build DPDK
ADD uname /root/bin/uname


ENV HOSTNAME odp-fedora-22

ENTRYPOINT /bin/bash
