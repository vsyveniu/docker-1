FROM node:carbon

WORKDIR /app

COPY package*.json ./

RUN yarn install

COPY /Users/vsyveniu/projects/nodetest

EXPOSE 8080

CMD[ "node", "server.js" ]