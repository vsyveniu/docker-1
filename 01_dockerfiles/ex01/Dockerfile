FROM debian:latest
RUN apt-get -y update && apt-get -y upgrade
RUn apt-get install -y mariadb-client mariadb-server

RUN iptables -A INPUT -p udp --dport 9987 -j ACCEPT
RUN iptables -A INPUT -p udp --sport 9987 -j ACCEPT
RUN iptables -A INPUT -p tcp --dport 30033 -j ACCEPT
RUN iptables -A INPUT -p tcp --sport 30033 -j ACCEPT
RUN iptables -A INPUT -p tcp --dport 10011 -j ACCEPT
RUN iptables -A INPUT -p tcp --sport 10011 -j ACCEPT

//RUN adduser teamspeak
//RUN su teamspeak
//RUN cd /home/teamspeak



RUN apt-get update
RUN apt-get install bzip2

RUN wget http://dl.4players.de/ts/releases/3.0.13.8/teamspeak3-server_linux_amd64-3.0.13.8.tar.bz2
RUN user@server:~$ tar xfvj teamspeak3-server_linux_amd64-3.0.13.8.tar.bz2