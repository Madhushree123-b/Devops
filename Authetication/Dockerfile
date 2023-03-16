FROM node:19-alpine

WORKDIR /Authetication

COPY package.json .

RUN npm install

RUN npm uninstall bcrypt

RUN npm install bcrypt

COPY . .

EXPOSE 3000

CMD ["npm" , "start"]

