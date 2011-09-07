# PHP 5.3 FPM

[PHP FPM] [0] is an awesome way of running PHP as a CGI. I have only ever used it with Nginx, but it can
be used with any web server that supports FCGI.

## Prereqs

	libgd2-xpm libgd2-xpm-dev libxml2-dev libcurl4-dev libmcrypt-dev

## Configure the build

	./configure \
	  --prefix=/usr/local \
	  --enable-cli \
	  --enable-shared=all \
	  --with-zlib \
	  --with-curl \
	  --enable-ftp \
	  --with-openssl=/usr \
	  --with-gd \
	  --with-mcrypt \
	  --with-mysql=mysqlnd \
	  --with-mysqli=mysqlnd \
	  --with-pdo-mysql=mysqlnd \
	  --enable-mbstring \
	  --enable-fpm

## Install

	make && make install
	
## Configure the server

To set up init.d to start PHP FPM:

	sudo cp sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm

To add a configuration for FPM, just copy the recommended file for FPM:

BASH:

	cp api/fpm/php-fpm.conf /usr/local/php.ini

Edit accordingly and profit!

## To use with Nginx

Here is a basic /etc/nginx/nginx.conf to use with FPM:

	user  www-data;
	worker_processes  2;

	error_log  logs/error.log;
	#error_log  logs/error.log  notice;
	#error_log  logs/error.log  info;

	#pid        logs/nginx.pid;


	events {
	    worker_connections  1024;
	}


	http {
	    include       mime.types;
	    default_type  application/octet-stream;

	    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
	                      '$status $body_bytes_sent "$http_referer" '
	                      '"$http_user_agent" "$http_x_forwarded_for"';

	    access_log  logs/access.log  main;

	    sendfile        on;
	    tcp_nopush     on;

	    #keepalive_timeout  0;
	    keepalive_timeout  65;

	    gzip  on;
	    gzip_min_length 1000;
	    gzip_proxied expired no-cache no-store private auth;
	    gzip_types  text/plain application/xml application/json text/json application/javascript text/javascript text/css;
	    gzip_disable "MSIE [1-6]\.";

	    include /etc/nginx/sites/*;

	}

Here is a basic Nginx Virtualhost:

	server {
		server_name mysite.com;
		index index.php;
		root /var/www/docroot;
	
		location ~ .php$ {
			fastcgi_index index.php;
			fastcgi_pass 127.0.0.1:9000;
			include /etc/nginx/fastcgi_params;
			fastcgi_param SCRIPT_FILENAME /var/www/docroot$fastcgi_script_name;		
		}
	
		location ~* ^.+.(jpg|jpeg|gif|css|png|js|ico|html|xml|txt)$ {
		    access_log off;
		    expires 30d;
		}
	
	}

[0]: http://php-fpm.org/