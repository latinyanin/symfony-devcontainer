FROM php:8.3-cli

# Dependencies
RUN apt-get update \
    && apt-get install -y \
    git \
    libicu-dev \
    libpq-dev \
    libzip-dev \
    unzip \
    wget \
    sudo \
    zip \
    curl \
    less \
    zsh \
    zsh-autosuggestions \
    bash-completion \
    default-mysql-client \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install xdebug
RUN yes | pecl install xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.mode = debug" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.start_with_request = yes" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.client_port = 9000" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.log = /dev/null" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && rm -rf /tmp/pear

# PHP Extensions
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions \
    bcmath \
    gd \
    intl \
    pdo \
    pdo_mysql \
    zip


# Install composer
RUN curl -sSL https://getcomposer.org/installer | php \
    && chmod +x composer.phar \
    && mv composer.phar /usr/local/bin/composer

# Symfony CLI
RUN wget https://get.symfony.com/cli/installer -O - | bash \
    && mv /root/.symfony*/bin/symfony /usr/local/bin/symfony

# Working directory
WORKDIR /workspaces
