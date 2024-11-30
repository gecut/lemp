# Use a lightweight WordPress image
FROM wordpress:6.6-php8.2-fpm

WORKDIR /var/www/html
EXPOSE 80

ENV WORDPRESS_DB_HOST=db:3306
ENV WORDPRESS_DB_USER=$MYSQL_USER
ENV WORDPRESS_DB_PASSWORD=$MYSQL_PASSWORD
ENV WORDPRESS_DB_NAME=$MYSQL_DATABASE

COPY php.conf.ini $PHP_INI_DIR/conf.d/
COPY fix-perms.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/fix-perms.sh

ARG APT_INSTALL
RUN set -ex; \
  if [ -z "$APT_INSTALL" ]; then \
    echo "Skip apt packages: $APT_INSTALL"; \
  else \
    echo "Installing apt packages"; \
    apt-get update -y; \
    apt-get install -y --no-install-recommends $APT_INSTALL; \
    apt-get autoremove -y; \
    apt-get clean -y; \
    rm -rfv /var/lib/apt/lists/*; \
  fi
ARG PHP_EXT_INSTALL
RUN set -ex; \
  if [ -z "$PHP_EXT_INSTALL" ]; then \
    echo "Skip php extensions"; \
  else \
    echo "Installing php extensions: $PHP_EXT_INSTALL"; \
    docker-php-ext-install $PHP_EXT_INSTALL; \
  fi

ARG SOURCEGUARDIAN_LOADER=0
RUN set -ex; \
  if [ "$SOURCEGUARDIAN_LOADER" != "1" ]; then \
    echo "Skip sourceguardian loader"; \
  else \
    echo "Installing sourceguardian loader"; \
    PHP_EXT_DIR=$(php -i | grep -oP 'extension_dir\s*=\s*\K.*'); \
    mkdir -p /tmp/sourceguardian; \
    cd /tmp/sourceguardian; \
    curl -sSLO https://www.sourceguardian.com/loaders/download/loaders.linux-x86_64.tar.gz; \
    tar xzf loaders.linux-x86_64.tar.gz; \
    mv ixed.${PHP_VERSION}.lin "$PHP_EXT_DIR/sourceguardian.so"; \
    echo "extension=sourceguardian.so" > $PHP_INI_DIR/conf.d/15-sourceguardian.ini; \
    rm -rf /tmp/sourceguardian; \
  fi

ARG IONCUBE_LOADER=0

ENV IONCUBE_VERSION=13.3.0

RUN set -ex; \
  if [ "$IONCUBE_LOADER" != "1" ]; then \
    echo "Skip ioncube loader"; \
  else \
    PHP_EXT_DIR=$(php -i | grep '^extension_dir =' | cut -d' ' -f3); \
    echo "Installing ioncube loader"; \
    echo $(php -v); \
    echo "PHP_EXT_DIR = $PHP_EXT_DIR"; \
    mkdir -p /tmp/ioncube; \
    cd /tmp/ioncube; \
    IONCUBE_URL="http://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64_${IONCUBE_VERSION}.tar.gz" ; \
    curl -sSLO "$IONCUBE_URL"; \
    ls -lah; \
    tar xzf ioncube_loaders_lin_x86-64_${IONCUBE_VERSION}.tar.gz; \
    ls -lah ioncube/; \
    mv ioncube/ioncube_loader_lin_8.2.so "$PHP_EXT_DIR/ioncube.so"; \
    ls -lah "$PHP_EXT_DIR"; \
    echo "zend_extension=ioncube" > $PHP_INI_DIR/conf.d/16-ioncube.ini; \
    echo $(php -v); \
    rm -rf /tmp/ioncube; \
  fi
