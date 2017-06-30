FROM telegraf:alpine

RUN apk --no-cache add net-snmp-tools

COPY ./telegraf.conf /etc/telegraf/telegraf.conf
