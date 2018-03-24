
#container for a MEAN stack
#create a continer with mongodb before: docker run -p 27017:27017 --name=database -d mongo

FROM ubuntu:latest
EXPOSE 3000 27017 35729
RUN apt-get -q update && apt-get -y install \
	git \
	curl \
	ssh \
	gcc \
	make \
	build-essential \
	sudo \
	apt-utils  &&\
	apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - \
	&& apt-get -y install nodejs \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN npm install -g gulp \
	&& npm cache clean
RUN mkdir /usr/src/app
WORKDIR /usr/src/app
RUN npm install -g bower
RUN git clone https://github.com/meanjs/mean.git /usr/src/app
RUN npm install  && \
	npm cache clean
RUN bower install --config.interactive=false --allow-root

#need to connect to database somehow