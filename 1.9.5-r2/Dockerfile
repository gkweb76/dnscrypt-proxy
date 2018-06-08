# Base image is Alpine Linux
# docker build -t gkweb76/dnscrypt-proxy:1.9.5 -t gkweb76/dnscrypt-proxy:latest -t gkweb76/dnscrypt-proxy:1.9.5-r2 .
FROM alpine:3.7
LABEL maintainer="Guillaume Kaddouch"
LABEL twitter="@gkweb76"

# Install dnscrypt-proxy
RUN apk add --update --no-cache dnscrypt-proxy=1.9.5-r2 && \
    rm -rf /var/cache/apk/* /tmp/* /var/tmp/*

# Healtcheck
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 CMD nslookup dnscrypt.org || exit 1

# Environnement variables
ENV LOCAL_IP 0.0.0.0
ENV LOCAL_PORT 53
ENV SERVER dnscrypt.eu-dk

# Port available
EXPOSE $LOCAL_PORT/udp

# Version
ENV DNSCRYPT_VERSION 1.9.5-r2

# Start dnscrypt-proxy daemon based on ENV variables
CMD /usr/sbin/dnscrypt-proxy --local-address $LOCAL_IP:$LOCAL_PORT --resolver-name $SERVER --user=dnscrypt
