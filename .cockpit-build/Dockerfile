FROM php:7.2.24-apache
LABEL Patrick Williams <patrick.williams@mirumagency.com>
ARG COCKPIT_VERSION="master"

RUN apt-get update \
    && apt-get install -y \
	wget zip unzip \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        sqlite3 libsqlite3-dev \
        libssl-dev \
        libzip-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) iconv gd pdo zip opcache pdo_sqlite \
    && a2enmod rewrite expires

# install cockpit
RUN wget https://github.com/agentejo/cockpit/archive/${COCKPIT_VERSION}.zip -O /tmp/cockpit.zip; unzip /tmp/cockpit.zip -d /tmp/; rm /tmp/cockpit.zip
RUN mv /tmp/cockpit-${COCKPIT_VERSION}/.htaccess /var/www/html/.htaccess
RUN mv /tmp/cockpit-${COCKPIT_VERSION}/* /var/www/html/
RUN rm -R /tmp/cockpit-${COCKPIT_VERSION}/

# install monderation addon for workflows
RUN wget https://github.com/pauloamgomes/CockpitCMS-Moderation/archive/${COCKPIT_VERSION}.zip -O /tmp/CockpitCMS-Moderation.zip; unzip /tmp/CockpitCMS-Moderation.zip -d /tmp/; rm /tmp/CockpitCMS-Moderation.zip
RUN mkdir -p /var/www/html/addons/Moderation
RUN mv /tmp/CockpitCMS-Moderation-${COCKPIT_VERSION}/* /var/www/html/addons/Moderation/
RUN rm -R /tmp/CockpitCMS-Moderation-${COCKPIT_VERSION}/

# install cloud storage addon for AWS, Azure or Google storage
RUN wget https://github.com/agentejo/CloudStorage/archive/${COCKPIT_VERSION}.zip -O /tmp/CloudStorage.zip; unzip /tmp/CloudStorage.zip -d /tmp/; rm /tmp/CloudStorage.zip
RUN mkdir -p /var/www/html/addons/CloudStorage
RUN mv /tmp/CloudStorage-${COCKPIT_VERSION}/* /var/www/html/addons/CloudStorage/
RUN rm -R /tmp/CloudStorage-${COCKPIT_VERSION}/


RUN echo "\n\nphp_value post_max_size 256M" >> /var/www/html/.htaccess
RUN echo "\nphp_value  upload_max_filesize 256M" >> /var/www/html/.htaccess

COPY ./configs/php.ini /usr/local/etc/php/php.ini

RUN chown -R www-data:www-data /var/www/html