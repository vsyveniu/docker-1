FROM debian:latest
RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install curl \
					   wget \
					   git \
					   bzip2 \
					   gcc

WORKDIR $HOME/local
RUN wget https://dl.google.com/go/go1.9.4.linux-amd64.tar.gz
RUN tar -xvf go1.9.4.linux-amd64.tar.gz

ENV GOROOT=$HOME/local/go
ENV GOPATH=$HOME/gogs
ENV PATH=$PATH:$GOROOT/bin:$GOPATH/bin
WORKDIR $GOPATH/src/github.com/gogits
RUN cd $GOPATH/src/github.com/gogits
RUN git clone --depth=1 -b develop https://github.com/gogits/gogs
RUN go get -u -tags "sqlite" github.com/gogits/gogs
WORKDIR $GOPATH/src/github.com/gogits/gogs
RUN go build -tags "sqlite"
ENV USER=root
EXPOSE 3000
EXPOSE 22

CMD ["./gogs", "web"]

#docker run --name=gogs -p 3000:3000 -p 3022:22 -d <image id>
#need to set a domain 192.168.99.100 and change user to root