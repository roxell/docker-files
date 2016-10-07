############################################################
# Dockerfile to build devel container images
# Based on Debian
############################################################

# Set the base image to Debian
FROM roxell/debian-devel

# File Author / Maintainer
MAINTAINER anders.roxell@gmail.com

#
ENV DEBIAN_FRONTEND noninteractive

# Update the repository sources list
RUN apt-get update && \
    apt-get install -y \
    texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended \
    texlive-lang-swedish latex2html \
    doxygen graphviz asciidoctor source-highlight librsvg2-bin mscgen

# Cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
