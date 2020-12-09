FROM php:7.4.12-apache

# パッケージの更新とインストール
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        locales \
        vim \
    && apt-get -y clean \
    && rm -r /var/lib/apt/lists/*

# localeを日本に設定
RUN echo "ja_JP.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen \
    && update-locale LANG=ja_JP.UTF-8
ENV LANG ja_JP.UTF-8

# 日本時間を設定
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# composerをインストール
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
        --install-dir=/usr/local/bin \
        --filename=composer \
        --version=2.0.7 \
    && php -r "unlink('composer-setup.php');"

# apacheコンフィグファイルをコピー
COPY apache2 /etc/apache2

# composer install
# WORKDIR /var/www/html
# CMD composer install
