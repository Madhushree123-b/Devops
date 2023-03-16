FROM node:19-alpine

WORKDIR /PatientRegistration

COPY package.json .

RUN npm install

COPY . .

EXPOSE 6000

CMD ["npm" , "start"]

