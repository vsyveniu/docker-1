FROM debian:latest

RUN apt-get -y update && \
	apt-get -y install cron && \
	apt-get -y install openssh-server && \
	apt-get -y install openssh-client && \
	apt-get -y install vim && \
	apt-get -y install sudo

WORKDIR /init

RUN mkdir system && \
	mkdir scripts

COPY ./initgen/system /init/system	
COPY ./initgen/scripts /init/scripts	

ENTRYPOINT ["bash"]

#to copy files from container: docker cp <container name or id>:/pathtodestination /pathofsourceincontainer
#to create container: docker run -h <desired hostname> --name=example <image id>
#to exit container: exit13
#to launch again: docker container start -i <container id or name>

