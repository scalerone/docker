FROM nginx:1.13.3
ADD nginx.conf /etc/nginx/nginx.conf
RUN mkdir -p /opt/logs \
	&& mkdir -p /opt/application \
	&& chown -R www-data.www-data /opt
VOLUME ["/opt"]