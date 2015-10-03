############################################################
# Dockerfile to build perf_event_tests container images
# Based on Ubuntu
############################################################

# Set the base image to Ubuntu
FROM roxell/ubuntu-dev

# File Author / Maintainer
MAINTAINER anders.roxell@linaro.org

# Make sure apt-get isn't interactive
ENV DEBIAN_FRONTEND noninteractive

## Needed to build
ADD clone-and-build-perf-event-tests /root/bin/clone-and-build-perf-event-tests

ENV HOSTNAME perf-ubuntu-1504
