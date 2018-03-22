FROM  ruby:latest

RUN apt-get update && \
	apt-get -y upgrade && \
	apt-get -y install ruby-full && \
	gem install rails
			
COPY ./app/ /opt/app

ONBUILD RUN rake db:migrate
ONBUILD RUN rake db:populate
 

ENTRYPOINT ["bash"]