FROM node:8.16.0-jessie

WORKDIR /app

RUN  apt-get update && apt-get install make g++ git openrc dbus  avahi-daemon avahi-discover avahi-utils libnss-mdns mdns-scan -y

RUN apt-get install libavahi-compat-libdnssd-dev -y

COPY avahi-daemon.conf /etc/avahi

RUN git clone https://github.com/giejay/google-home-notification-gateway .

RUN apt-get install python

RUN npm install --only=production --build-from-source=bcrypt

VOLUME /app/backend/storage

EXPOSE 3000

COPY browser.js /app/node_modules/mdns/lib/browser.js

ADD public /app/public

CMD openrc boot && rc-service dbus start && rc-service avahi-daemon start && npm run start
