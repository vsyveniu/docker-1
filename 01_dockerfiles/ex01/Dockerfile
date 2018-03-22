FROM debian:latest
RUN apt-get update
RUN apt-get -y install bzip2
RUN apt-get -y install wget

RUN mkdir /teamspeak
RUN wget http://dl.4players.de/ts/releases/3.0.13.8/teamspeak3-server_linux_amd64-3.0.13.8.tar.bz2
RUN tar -xvf teamspeak3-server_linux_amd64-3.0.13.8.tar.bz2 -C /teamspeak
RUN cd /teamspeak/teamspeak3-server_linux_amd64/
EXPOSE 9987
EXPOSE 30033 
EXPOSE 10011 
EXPOSE 41144
ENTRYPOINT ["sh", "ts3server_minimal_runscript.sh"]



