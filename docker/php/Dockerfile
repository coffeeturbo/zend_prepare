FROM php:fpm

#ENV APP_USER jet



# Setup mysql
RUN docker-php-ext-install pdo pdo_mysql opcache > /dev/null

# Setup composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Setup ZIP
RUN \
    apt-get update > /dev/null && \
    apt-get install -y git zip unzip && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


# Setup GD
RUN apt-get update && \
    apt-get install -y libfreetype6-dev libjpeg62-turbo-dev && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/  &&  \
    docker-php-ext-install gd

# setup intl extension
RUN apt-get update \
  && apt-get install -y zlib1g-dev libicu-dev g++ \
  && docker-php-ext-configure intl \
  && docker-php-ext-install intl

# Setup user & symfony console

RUN echo "upload_max_filesize = 20M\n" > /usr/local/etc/php/conf.d/jet.ini

# setup mailer
#RUN apt-get update && apt-get install -q -y ssmtp mailutils && rm -rf /var/lib/apt/lists/*
#RUN echo "hostname=localhost.localdomain" > /etc/ssmtp/ssmtp.conf
#RUN echo "root=root@example.com" >> /etc/ssmtp/ssmtp.conf
#RUN echo "mailhub=smtp.gmail.com:587" >> /etc/ssmtp/ssmtp.conf
#RUN echo "UseTLS=Yes" >> /etc/ssmtp/ssmtp.conf
#RUN echo "UseStartTLS=Yes" >> /etc/ssmtp/ssmtp.conf
#RUN echo "AuthMethod=LOGIN" >> /etc/ssmtp/ssmtp.conf
#RUN echo "AuthUser=proyoozer@gmail.com" >> /etc/ssmtp/ssmtp.conf
#RUN echo "AuthPass=33626261p" >> /etc/ssmtp/ssmtp.conf
#RUN echo "FromLineOverride=yes" >> /etc/ssmtp/ssmtp.conf
#RUN echo "root:proyoozer@gmail.com:smtp.gmail.com:587" >> /etc/ssmtp/revaliases


RUN echo "sendmail_path=sendmail -i -t" >> /usr/local/etc/php/conf.d/php-sendmail.ini

RUN echo "localhost localhost.localdomain" >> /etc/hosts
