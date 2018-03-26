
#container for a MEAN stack
#create a continer with mongodb before: docker run -p 27017:27017 --name=db -d mongo

FROM debian:latest
EXPOSE 3000 27017 35729
RUN apt-get update && apt-get  -y upgrade
RUN apt-get -y install --allow-unauthenticated \
	git \
	curl \
	ssh \
	gcc \
	make \
	build-essential \
	sudo \
	apt-utils
RUN curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash - \
	&& apt-get -y install nodejs 
RUN npm install -g gulp 
RUN mkdir /usr/src/app
WORKDIR /usr/src/app
RUN npm install -g bower
RUN git clone https://github.com/meanjs/mean.git /usr/src/app
RUN npm install 
RUN bower install --config.interactive=false --allow-root

CMD ["npm", "start"]

#to create container for test: docker run --name=mean -p 3000:3000 -p 35729:35729 --link db:db_1 -i -t <image id or tag>