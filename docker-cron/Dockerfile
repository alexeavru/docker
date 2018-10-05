FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y python cron apt-utils locales tzdata

RUN echo "tzdata tzdata/Areas select Europe" > timezone.txt
RUN echo "tzdata tzdata/Zones/Europe select Moscow" >> timezone.txt
RUN debconf-set-selections timezone.txt
RUN rm /etc/timezone
RUN rm /etc/localtime
RUN dpkg-reconfigure -f noninteractive tzdata


RUN rm -rf /var/lib/apt/lists/*

RUN touch /var/log/cron.log

WORKDIR /var/www/html

#RUN echo "echo \"<h4>Hello from $(hostname) - '$(date)'</h4>\" >> /var/www/html/index.html" > /var/www/html/work.sh && chmod +x /var/www/html/work.sh
COPY work.sh /var/www/html/work.sh

RUN chmod +x /var/www/html/work.sh

RUN (crontab -l ; echo "* * * * * /var/www/html/work.sh") | crontab

CMD service cron start && python -m SimpleHTTPServer 8080



