FROM debian:bullseye
LABEL org.opencontainers.image.authors="vegard@loekken.org"

# Update distrib
RUN apt-get update

# Install necessary packages
RUN apt-get install -y nginx dnsmasq certbot curl cron

# Copy files
COPY docker /docker

# Copy configuration files
RUN cp /docker/config/nginx.conf /etc/nginx/ && \
    cp /docker/config/proxy.conf /etc/nginx/conf.d/

# Copy crontab
RUN cp /docker/crontab /etc/cron.d/certbot

# Volumes
VOLUME /etc/nginx/sites-enabled
VOLUME /etc/letsencrypt

# Environment variables
ENV LETSENCRYPT_EMAIL none
ENV STARTUP_WAIT 0

# Ports
EXPOSE 80
EXPOSE 443

# Command and healthcheck
CMD ["bash", "/docker/scripts/entrypoint.sh" ]
HEALTHCHECK CMD curl --fail http://localhost || exit 1
