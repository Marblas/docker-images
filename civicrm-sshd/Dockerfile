FROM docker-registry.siecobywatelska.pl/civicrm-php:latest@sha256:a4634132c6010066c28bc4d9fa669d18d9555e525754bb5a10b55de77db2e6c5
MAINTAINER Adam Dobrawy "http://github.com/ad-m/"
# Setup SSHD server
RUN apt-get update \
&& apt-get install -y --no-install-recommends openssh-server curl rsync wget git less nano \
&& rm -rf /var/lib/apt/lists/* \
&& mkdir /var/run/ssh /root/.ssh
USER root
EXPOSE 22
# Add github ssh-keys importer
ENV ACCESS_USER="root,www-data"
COPY ./entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

# Add wp-cli
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
&& php wp-cli.phar --info \
&& chmod +x wp-cli.phar \
&& mv wp-cli.phar /usr/local/bin/wp
RUN mkdir /var/www/.ssh \
&& chown www-data:www-data /var/www/.ssh

# Add mariadb-client
RUN apt-get update \
&& apt-get install -y --no-install-recommends mariadb-client \
&& rm -rf /var/lib/apt/lists/*

# Add persistent sshd keys
ENV SSH_KEYS_DIR="/etc/ssh-keys"
VOLUME /etc/ssh-keys
RUN usermod --shell /bin/bash www-data
RUN chown www-data:www-data /etc/ssh-keys
RUN sed -e 's@#*HostKey /etc/ssh/ssh_host_@HostKey /etc/ssh-keys/ssh_host_@g' -i /etc/ssh/sshd_config
CMD ["/usr/sbin/sshd", "-D"]
