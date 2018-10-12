FROM node:latest
MAINTAINER Angelo Ferreira
COPY . /var/www/
WORKDIR /var/www/
RUN npm install
ENTRYPOINT ["npm", "start"]
EXPOSE 3000
