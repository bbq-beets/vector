FROM docker.io/library/debian:bullseye

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
  && apt-get -y --no-install-recommends install apt-utils apt-transport-https lsb-release ca-certificates curl wget \
  && wget -O /etc/apt/trusted.gpg.d/bind.gpg https://packages.sury.org/bind/apt.gpg \
  && sh -c 'echo "deb https://packages.sury.org/bind/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/bind.list' \
  && apt-get update \
  && apt-get -y --no-install-recommends install bind9 bind9utils dnsutils \
  && apt-get remove --autoremove -y apt-utils apt-transport-https lsb-release ca-certificates curl wget \
  && rm -rf /var/list/apt/lists/*

COPY named.conf.local /etc/bind/
COPY db.example.com /var/lib/bind/
COPY nsupdate.txt /bind3/etc/bind/
COPY named.conf.options.template /etc/bind/
COPY configure_bind.sh /etc/bind/
RUN chmod +x /etc/bind/configure_bind.sh

CMD ["/etc/bind/configure_bind.sh"]
