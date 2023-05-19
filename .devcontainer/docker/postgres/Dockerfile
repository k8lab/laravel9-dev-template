FROM postgres:14.7-alpine

ARG TIME_ZONE

ENV TZ=${TIME_ZONE}

RUN apk update && apk add --no-cache --virtual .build-dependencies tzdata \
    && cp /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime \
    && apk del --no-network .build-dependencies