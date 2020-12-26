# why ubuntu:20.04 and not node:alpine?
# cause alpine in docker don't play good with ipv6
# and apk will hang when its fetch returns dual-stack.
FROM ubuntu:20.04

USER root

WORKDIR {{ lirc_web_app_path }}

# Preconfigure debconf for non-interactive installation - otherwise complains about terminal
# Avoid ERROR: invoke-rc.d: policy-rc.d denied execution of start.
ARG DEBIAN_FRONTEND=noninteractive
ENV DISPLAY localhost:0.0
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections \
	&& dpkg-divert --local --rename --add /sbin/initctl \
	&& ln -sf /bin/true /sbin/initctl \
	&& echo "#!/bin/sh\nexit 0" > /usr/sbin/policy-rc.d

# set timezone (for interactive environments)
# tzdata will be installed by node.js dependencies,
# so just configure the timezone now
RUN echo "{{ default_timezone }}" > /etc/timezone

# install prerequisites: lirc, node, npm
RUN apt-get update -q \
  && apt-get -q -y -o "DPkg::Options::=--force-confold" -o "DPkg::Options::=--force-confdef" install --upgrade lirc nodejs npm \
  && apt-get -q -y autoremove \
  && apt-get -q -y clean \
  && rm -rf /var/lib/apt/lists/*

# install lirc_web
RUN npm install -g lirc_web

# apply lirc_web patch to resolve empty remote commands
# due to a race condition
COPY lirc_node.js.diff .
RUN  patch {{ lirc_web_node_path }}/node_modules/lirc_node/lib/lirc_node.js lirc_node.js.diff

ENTRYPOINT lirc_web
