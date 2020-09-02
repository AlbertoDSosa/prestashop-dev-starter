FROM prestashop/prestashop:1.7-7.3-apache
LABEL manteiner="Alberto D.Sosa <albertodsosa@gmail.com>"

RUN pecl install xdebug-2.9.6 && docker-php-ext-enable xdebug

RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini

RUN useradd albertodsosa

