############################################################
# Dockerfile to build devel container images
# Based on Debian
############################################################

# Set the base image to Debian
FROM debian:stretch

# File Author / Maintainer
MAINTAINER anders.roxell@gmail.com

#
ENV DEBIAN_FRONTEND noninteractive

# Update the repository sources list
RUN apt-get update

# Install base packages
RUN apt-get update && \
    apt-get install -y build-essential git lib32stdc++6 \
    lib32z1 gcc-multilib curl wget vim-nox gdb strace zsh \
    rxvt-unicode-256color lcov autoconf automake libtool \
    doxygen graphviz libssl-dev libcunit1-dev clang-3.9 \
    fakeroot dpkg-dev bc tmux sudo keychain procps

# Setup home environment
RUN useradd -b /home/ -m -s /bin/zsh devel && echo "devel:docker" | chpasswd
ENV PATH /home/devel/bin:$PATH
RUN usermod -aG sudo devel

WORKDIR /home/devel
ENV HOME /home/devel
ENV USER devel

ADD uname /usr/local/bin/uname
RUN mkdir /home/devel/.ssh

RUN ln -sf /home/devel/etc/zsh/zshrc          /home/devel/.zshrc
RUN ln -sf /home/devel/etc/dir_colors         /home/devel/.dir_colors
RUN ln -sf /home/devel/etc/vim                /home/devel/.vim
RUN ln -sf /home/devel/etc/vim/vimrc          /home/devel/.vimrc
RUN ln -sf /home/devel/etc/bash/bashrc        /home/devel/.bashrc
RUN ln -sf /home/devel/etc/bash/bash_profile  /home/devel/.bash_profile
RUN ln -sf /home/devel/etc/bash/bash_logout   /home/devel/.bash_logout
RUN ln -sf /home/devel/etc/git/gitconfig      /home/devel/.gitconfig
RUN ln -sf /home/devel/etc/git/gitignore      /home/devel/.gitignore
RUN ln -sf /home/devel/etc/gdbinit            /home/devel/.gdbinit
RUN ln -sf /home/devel/etc/bash               /home/devel/.bash
RUN ln -sf /home/devel/etc/shell              /home/devel/.shell
RUN ln -sf /home/devel/etc/zsh                /home/devel/.zsh
RUN ln -sf /home/devel/etc/toprc              /home/devel/.toprc
RUN ln -sf /home/devel/etc/tmux/tmux.conf     /home/devel/.tmux.conf
RUN ln -sf /home/devel/etc/urxvt              /home/devel/.urxvt
RUN ln -sf /home/devel/etc/ssh_config         /home/devel/.ssh/config

# Cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV SHELL /bin/zsh
ENV LC_ALL=C

ENTRYPOINT /bin/zsh
