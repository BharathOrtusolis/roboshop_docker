FROM node:20

WORKDIR /opt/server

COPY package*.json ./

RUN npm install

COPY . .

ENV MONGO=true \
    MONGO_URL=mongodb://mongodb:27017/catelogue

CMD ["node", "server.js"]