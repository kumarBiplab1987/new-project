From    ubuntu:20.04

# Configure apt
run     echo 'deb http://us.archive.ubuntu.com/ubuntu/ trusty universe' >> /etc/apt/sources.list
run     apt-get -y update

# Install prereqs
run     apt-get install -y \
    apache2 \
    mysql-server \
    php \
    php-mysql \
    libapache2-mod-php \
    php-xml \
    php-mbstring \
    php-apcu \
    php-intl \
    imagemagick \
    inkscape \
    php-gd \
    php-cli \
    php-curl \
    php-bcmath \
    git

# Install mediawiki
add     https://releases.wikimedia.org/mediawiki/1.39/mediawiki-1.39.0.tar.gz /tmp/mediawiki.tgz
run     cd /tmp  && tar zxf mediawiki.tgz
run     mkdir /var/lib/mediawiki
run     mv mediawiki-*/* /var/lib/mediawiki
run     ln -s /var/lib/mediawiki /var/www/html/mediawiki

# Add startup script
add     ./mediawiki-start /usr/bin/mediawiki-start

expose  80
cmd     ["/usr/bin/mediawiki-start"]
