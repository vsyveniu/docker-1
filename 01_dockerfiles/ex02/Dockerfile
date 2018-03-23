FROM  ruby:latest

RUN apt-get update && \
	apt-get -y upgrade && \
	apt-get -y install ruby-full && \
	apt-get -y autoclean && \
	gem install rails

			
ONBUILD COPY ./myapp/ /opt/app

ONBUILD WORKDIR /opt/app

ONBUILD RUN bundle install
ONBUILD RUN rake db:migrate
ONBUILD RUN rake db:populate
 

ENTRYPOINT ["bash"]