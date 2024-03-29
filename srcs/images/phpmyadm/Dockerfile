# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Dockerfile                                         :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: kiborroq <kiborroq@kiborroq.42.fr>         +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2021/02/10 20:41:07 by kiborroq          #+#    #+#              #
#    Updated: 2021/02/18 00:28:01 by kiborroq         ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

# Install OS
FROM alpine:3.12

# Install necessary components
RUN apk -U upgrade
RUN apk add nginx
RUN apk add wget
RUN apk add php7 php7-fpm php7-mbstring php7-zlib php7-json php7-session php7-mysqli php7-curl
RUN apk add supervisor
RUN wget http://files.directadmin.com/services/all/phpMyAdmin/phpMyAdmin-5.0.4-all-languages.tar.gz

# Adjust NGINX
RUN mkdir /run/nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Adjust PHPMYADMIN
RUN mkdir -p /www/phpmyadmin
RUN tar -xf phpMyAdmin-5.0.4-all-languages.tar.gz --strip-components 1 -C /www/phpmyadmin
RUN rm phpMyAdmin-5.0.4-all-languages.tar.gz
COPY phpmyadmin.conf /www/phpmyadmin/config.inc.php

# Adjut SUPERVISORD
COPY supervisord.conf /etc/supervisord.conf

# Declarate ports
EXPOSE 5000

ENTRYPOINT ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]