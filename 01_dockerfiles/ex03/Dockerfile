FROM debian:latest

RUN apt-get update && apt-get -y upgrade && \
	apt-get -y install git && \
	apt-get -y install wget && \
	apt-get -y install ca-certificates &&\
	apt-get -y install openssh-server && \
	apt-get -y install apt-transport-https && \
	apt-get -y install curl && \
	apt-get -y install gnupg && \
	apt-get -y install systemd 

RUN wget -q -O - https://packages.gitlab.com/gpg.key | apt-key add -
RUN apt-get update
RUN curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash
RUN echo 'deb https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu/ xenial main' >> /etc/apt/sources.list.d/gitlab_gitlab-ce.list && echo 'deb-src https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu/ xenial main' >> /etc/apt/sources.list.d/gitlab_gitlab-ce.
RUN apt-get -y install  --no-install-recommends gitlab-ce



EXPOSE 443 80 22

VOLUME ["/etc/gitlab", "/var/opt/gitlab", "/var/log/gitlab"]

RUN chmod 2770 /opt/gitlab/git-data && chown git:git /opt/gitlab/git-data

RUN gitlab-ctl reconfigure

