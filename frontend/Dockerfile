FROM node:18-alpine3.18
WORKDIR /my_application
COPY package*.json /my_application
RUN npm install
COPY . /my_application
CMD npm run dev -- --host 0.0.0.0