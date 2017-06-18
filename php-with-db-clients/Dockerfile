FROM php:7.1.6-apache

MAINTAINER Hamid Alaei <hamid.a85@gmail.com>

# Clean apt
RUN rm /var/lib/apt/lists/* -vrf && \
    apt-get clean

# MySql pre-install configuration
RUN set -ex; \
# gpg: key 5072E1F5: public key "MySQL Release Engineering <mysql-build@oss.oracle.com>" imported
	key='A4A9406876FCBD3C456770C88C718D3B5072E1F5'; \
	export GNUPGHOME="$(mktemp -d)"; \
	gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
	gpg --export "$key" > /etc/apt/trusted.gpg.d/mysql.gpg; \
	rm -r "$GNUPGHOME"; \
	apt-key list > /dev/null

# MySql & Mongo pre-install configuration
RUN \
    echo "deb http://repo.mysql.com/apt/debian/ jessie mysql-5.7" > /etc/apt/sources.list.d/mysql.list && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6 && \
    echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/3.4 main" | \
        tee /etc/apt/sources.list.d/mongodb-org-3.4.list && \
    apt-get update && \
# Installing packages
    apt-get install -yq --force-yes --fix-missing \
    mongodb-org-shell mongodb-org-tools \
    mysql-client
