FROM prestashop/prestashop:1.6-7.2-apache
LABEL manteiner="Alberto D.Sosa <albertodsosa@gmail.com>"

RUN pecl install xdebug-2.9.6 && pecl install mcrypt-1.0.3 && docker-php-ext-enable xdebug mcrypt

RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini

RUN useradd <local_user> && useradd 1001

