# docker build -t kalabox/php-appserver:stable .

FROM kalabox/nginx:v0.9.0

RUN \
  apt-get -y update && \
  apt-get -y install php5-cli libgmp10 libpng12-0 libjpeg8 libltdl7 libmcrypt4 libpq5 libicu48 libxslt1.1 && \
  cd /tmp && \
  curl -L -O https://github.com/phpbrew/phpbrew/raw/master/phpbrew && \
  chmod +x /tmp/phpbrew && \
  mv /tmp/phpbrew /usr/bin/phpbrew && \
  phpbrew init && \
  echo "source /root/.phpbrew/bashrc" >> /root/.bashrc && \
  ln -s /.phpbrew /root/.phpbrew && \
  apt-get update -y && \
  apt-get install -y unzip curl rsync git-core && \
  apt-get clean -y && \
  apt-get autoclean -y && \
  apt-get autoremove -y && \
  rm -rf /var/lib/apt/* && rm -rf && rm -rf /var/lib/cache/* && rm -rf /var/lib/log/* && rm -rf /tmp/*

RUN \
  cd /root/.phpbrew && \
  curl -L "http://github.com/kalabox/phpbrewer/releases/download/v0.2.1/php.tar.gz" | tar -zvx && \
  rm /root/start.sh

ENV PHP_VERSION 5.4.40

COPY start.sh /root/start.sh
RUN chmod +x /root/start.sh

CMD ["/root/start.sh"]

EXPOSE 80
EXPOSE 443
