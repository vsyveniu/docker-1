FROM debian:latest

RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install curl
RUN apt-get -y install gnupg
RUN curl -sL https://deb.nodesource.com/setup_9.x | bash -
RUN	apt-get -y install nodejs
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN apt-get -y install yarn


