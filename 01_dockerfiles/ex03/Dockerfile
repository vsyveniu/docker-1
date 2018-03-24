FROM debian:latest

RUN apt-get update && apt-get upgrade && \
	apt-get -y install git && \
	apt-get -y install wget && \
	apt-get -y install openssh-server && \
	apt-get -y install apt-transport-https && \
	apt-get -y install gnupg

RUN wget -q -O - https://packages.gitlab.com/gpg.key | apt-key add -
RUN apt-get -y install gitlab-ce


