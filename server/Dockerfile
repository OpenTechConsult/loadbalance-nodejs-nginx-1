FROM node:21.4.0-alpine3.18

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 5050

CMD [ "node", "index.js" ]