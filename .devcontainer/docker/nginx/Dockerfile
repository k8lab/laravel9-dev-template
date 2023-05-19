FROM nginx:1.23.4-alpine

ARG TIME_ZONE=Asia/Tokyo

ENV TZ=${TIME_ZONE}

RUN apk update && apk add --no-cache --virtual .build-dependencies tzdata openssl \
    && cp /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime \
    && openssl req -newkey rsa:2048 -x509 -nodes -set_serial 1 -days 3650 \
       -subj "/C=JP/ST=Aichi/L=Nagoya" \
       -keyout "/etc/ssl/private/server.key" -out "/etc/ssl/private/server.crt" \
    && chmod 400 /etc/ssl/private/server.* \
    && apk del --no-network .build-dependencies