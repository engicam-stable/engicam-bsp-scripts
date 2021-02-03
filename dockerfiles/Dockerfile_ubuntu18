FROM ubuntu:18.04
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get -y upgrade

# Essential Yocto Project host packages are:
RUN apt-get update
RUN apt-get install -y gawk wget git-core diffstat unzip texinfo gcc-multilib \
          build-essential chrpath socat cpio python python3 python3-pip python3-pexpect \
          xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev \
          pylint3 xterm rsync

# Additional host packages required by poky/scripts/wic
RUN apt-get install -y curl dosfstools mtools parted syslinux tree tzdata vim libtool libsdl2-2.0-0 \
          linux-headers-5.4.0-54-generic linux-image-5.4.0-54-generic
# Add "repo" tool (used by many Yocto-based projects)
RUN curl http://storage.googleapis.com/git-repo-downloads/repo > /usr/local/bin/repo
RUN chmod a+x /usr/local/bin/repo

RUN apt-get install -y git kernel-package fakeroot libncurses5-dev libssl-dev ccache lzop
# Create user "user"
RUN id user 2>/dev/null || useradd --uid 1000 --create-home user

# Create a non-root user that will perform the actual build
RUN apt-get install -y sudo
RUN echo "user ALL=(ALL) NOPASSWD: ALL" | tee -a /etc/sudoers

# Fix error "Please use a locale setting which supports utf-8."
# See https://wiki.yoctoproject.org/wiki/TipsAndTricks/ResolvingLocaleIssues
RUN apt-get install -y locales
RUN dpkg-reconfigure locales
RUN locale-gen en_US.UTF-8
RUN update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

ENV LANG en_US.UTF-8
USER user
CMD "/bin/bash"

# EOF