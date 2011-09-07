# Nginx

## Notes
I used the Debian layout for this configuration. If I ever do this again, I'll update the
layout to just stick everything in /usr/local.

## Prereqs

	libpcre3-dev libssl-dev

## Configure the build
	./configure \
	  --prefix=/usr/local \
	  --sbin-path=/usr/local/sbin \
	  --conf-path=/etc/nginx/nginx.conf \
	  --error-log-path=/var/log/nginx/error.log \
	  --pid-path=/var/run/nginx.pid \
	  --lock-path=/var/lock/nginx.lock \
	  --http-log-path=/var/log/nginx/access.log \
	  --with-http_dav_module \
	  --http-client-body-temp-path=/var/lib/nginx/body \
	  --with-http_ssl_module \
	  --http-proxy-temp-path=/var/lib/nginx/proxy \
	  --with-http_stub_status_module \
	  --http-fastcgi-temp-path=/var/lib/nginx/fastcgi \
	  --with-debug \
	  --with-http_flv_module

## Install
	
	make && make install
	
## Server configuration

To set up ini.d, just grab the Ubuntu init.d script from the [Nginx website] [0].

To configure Nginx, edit the configuration files in /etc/nginx

[0]: http://wiki.nginx.org/Nginx-init-ubuntu