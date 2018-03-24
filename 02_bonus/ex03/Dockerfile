#environment with node.js and express with hello worl exaple

FROM debian:latest

RUN mkdir /hello

WORKDIR /hello

RUN apt-get update && \
	apt-get -y upgrade
RUN apt-get -y install curl sudo gnupg
RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - \
	&& apt-get -y install nodejs \
	&& apt-get clean
RUN npm install express --save

COPY ./hello /hello

EXPOSE 8081

CMD ["node", "index.js"]


#docker run --name=<example> -p 8081:8081 -d <image id>