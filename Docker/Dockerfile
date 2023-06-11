# Use Ubuntu base image
FROM ubuntu:latest

# Set noninteractive environment
ENV DEBIAN_FRONTEND=noninteractive

# Update and upgrade packages
RUN apt update && apt upgrade -y

# Install Apache, MariaDB, PHP, and other required packages
RUN apt-get install -y apache2 php php-mysql libapache2-mod-php php-xml php-mbstring php-intl wget

WORKDIR /tmp

# Download MediaWiki tarball
RUN wget https://releases.wikimedia.org/mediawiki/1.39/mediawiki-1.39.3.tar.gz

# Extract MediaWiki tarball
RUN tar -xvzf /tmp/mediawiki-*.tar.gz

# Move MediaWiki files to appropriate directory
RUN mkdir /var/lib/mediawiki
RUN mv mediawiki-*/* /var/lib/mediawiki

COPY LocalSettings.php /var/www/html/mediawiki/

# Create symbolic link for MediaWiki in Apache's HTML directory
RUN ln -s /var/lib/mediawiki /var/www/html/mediawiki

# Expose port 80 for Apache
EXPOSE 80

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

RUN service apache2 restart

# Start Apache service
CMD ["apachectl", "-D", "FOREGROUND"]
