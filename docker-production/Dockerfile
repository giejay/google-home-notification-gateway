FROM node:8-alpine

WORKDIR /app

RUN  apk update && apk --no-cache add make g++ git openrc dbus avahi avahi-compat-libdns_sd avahi-dev

COPY avahi-daemon.conf /etc/avahi

RUN git clone https://github.com/giejay/google-home-notification-gateway .

RUN apk add python

RUN npm install --only=production --build-from-source=bcrypt

VOLUME /app/backend/storage

EXPOSE 3000

COPY browser.js /app/node_modules/mdns/lib/browser.js

CMD openrc boot && rc-service dbus start && rc-service avahi-daemon start && npm run start
