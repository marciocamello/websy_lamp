FROM phpdockerio/php71-fpm:latest

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install  php-memcached php7.1-mysql php7.1-pgsql php-redis php7.1-sqlite3 php7.1-bcmath php7.1-bz2 php7.1-dba php7.1-enchant php7.1-gd php-gearman php7.1-gmp php-igbinary php7.1-imap php-imagick php7.1-interbase php7.1-intl php7.1-ldap php7.1-mbstring php-msgpack php7.1-odbc php7.1-phpdbg php7.1-pspell php-raphf php7.1-recode php7.1-soap php-ssh2 php7.1-sybase php7.1-tidy php7.1-xmlrpc php7.1-xsl php-yaml php-tideways php-xhprof php-xdebug php-zmq \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*


WORKDIR "/home"