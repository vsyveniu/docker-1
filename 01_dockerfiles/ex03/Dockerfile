FROM debian:latest

RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install curl \
					   wget \
					   git \
					   bzip2
RUN wget https://dl.google.com/go/go1.9.4.linux-amd64.tar.gz
RUN tar -xvf go1.9.4.linux-amd64.tar.gz
RUN echo 'export GOROOT=$HOME/go' >> $HOME/.bashrc
RUN echo 'export GOPATH=$HOME/go' >> $HOME/.bashrc
RUN echo 'export PATH=$PATH:$GOROOT/bin:$GOPATH/bin' >> $HOME/.bashrc
RUN git clone --depth=1 -b develop https://github.com/gogits/gogs