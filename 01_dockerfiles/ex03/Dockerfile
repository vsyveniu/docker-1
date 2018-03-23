FROM debian:latest

RUN apt-get update && apt-get upgrade && \
	apt-get -y install git && \
	apt-get -y install wget

RUN git clone https://gitlab.com/gitlab-org/gitlab-ce.git gitlabce
