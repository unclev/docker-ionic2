# Ionic 2 developer container
# Use at your own risk! I have not tested any deployment, created my own as all the others did not work!
# alias ionic="docker-compose run --rm --service-ports dev ionic"
# then use ionic serve on localhost:8100

FROM ubuntu:16.04

MAINTAINER Victor Kulichenko <onclev@gmail.com>

ARG PUID
ARG PGID
ENV IUSER="ionicdev" PUID=${PUID:-1000} PGID=${PGID:-1000} \
    IONIC_BRANCH=${IONIC_BRANCH:-2} \
    PROJECTNAME=${PROJECTNAME}

# Set one or more individual labels
LABEL Description="Ionic 2 Framework Dev container" \
      Volumes="/home/$IUSER" \
      Ports="8100, 35729" \
      Ionic_Framework_Version="2.0.0" \
      Cordova_CLI_Version="6.5.0" \
      Ionic_CLI_Version="2.2.1" \
      Ionic_App_Lib_Version="2.2.0" \
      Ionic_App_Script_Version="1.0.0" \
      Node_Version="7.x" \
      TypeScript_Version="2.2.1" \
      release-date="2017-03-23" \
      is-production="False" \
      HOST_ALIAS="docker-compose run --rm --service-ports dev ionic"

RUN apt-get update && apt-get install -y -q curl \
 && curl -sL https://deb.nodesource.com/setup_7.x | bash - \

# install nodejs, npm, git, and sudo
 && apt-get install -y -q \
            nodejs \
            git \
            sudo \
 && apt-get -y autoclean \
 && rm -rf /var/lib/apt/lists/* \
# ionicdev sudouser and group
 && groupadd -g $PGID $IUSER && useradd -m -g $PGID -u $PUID -s /bin/bash $IUSER \
 && echo "%$IUSER ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

USER $IUSER

# install ionic, cordova, typescript, gulp
RUN sudo npm install -g -y ionic cordova typescript gulp \
 && echo n | cordova -v

# populate ionicdev home directory with a project(s) if it/they exists(s)
WORKDIR "/home/$IUSER"
COPY ${PROJECTNAME:-.} ./$PROJECTNAME
# the docker folder does not relate to the project
RUN sudo rm -R ./docker \
 && sudo chown -Rv $IUSER:$IUSER .

EXPOSE 8100 35729

# Do NOT use VOLUME statement as it may result in orphaned volumes ...
# docker run --rm ... bash
# VOLUME /myApp
