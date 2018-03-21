FROM debian:latest
RUN apt-get update
RUN apt-get -y install bzip2

RUN mkdir /teamspeak
RUN cd teamspeak
RUN wget http://dl.4players.de/ts/releases/3.0.13.8/teamspeak3-server_linux_amd64-3.0.13.8.tar.bz2
RUN tar -xvf teamspeak3-server_linux_amd64-3.0.13.8.tar.bz2
RUN cd teamspeak3-server_linux_amd64
RUN ./ts3server_startscript.sh start

