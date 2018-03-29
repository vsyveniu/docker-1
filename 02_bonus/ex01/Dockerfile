FROM debian:latest

RUN apt-get update && \
	apt-get clean
RUN useradd swag && mkdir -p /home/swag &&\
	chown swag:swag /home/swag
RUN apt-get install -y x11vnc && \
	apt-get install -y xvfb && \
	apt-get install -y fluxbox && \
	apt-get install -y wget && \
	apt-get install -y wmctrl && \
	apt-get install -y gnupg
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list
RUN apt-get update && \
	apt-get -y install google-chrome-stable
COPY ./boots.sh /
COPY ./testapp /testapp

CMD ["sh", "/boots.sh"]

#to run a container: docker run --name=<name> -p 5900:5900 -e VNC_SERVER_PASSWORD=root --user swag --privileged -d
#to run vnc: open vnc://192.168.99.100:5900
#to open testhtml via chrome: cd testapp && google-chrome ./index.html
