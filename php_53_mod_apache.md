# PHP 5.3 with mod_apache

## Compile some prerequisites

(or just use Homebrew;) )

[libmcrypt] [0]
download source, extract

BASH:

	./configure
	make
	sudo make install


[libjpg] [1]
download source, extract

BASH:
	./configure --enable-shared
	make
	sudo make install



[freetype] [2]
download source, extract

BASH:

	./configure
	make
	make (again)
	sudo make install


[libpng] [3]
download source, extract

	./configure
	make
	sudo make install

## Compile, install PHP

BASH:

	./configure \
	  --prefix=/usr/local/php53 \
	  --enable-cli \
	  --bindir=/usr/local/bin \
	  --with-apxs2=/usr/local/apache2/bin/apxs \
	  --enable-shared=all \
	  --with-zlib \
	  --with-curl \
	  --enable-ftp \
	  --with-openssl=/usr \
	  --with-freetype-dir=/usr/local \
	  --with-jpeg-dir=/usr/local/lib \
	  --with-png-dir=/usr/local \
	  --with-gd \
	  --with-mcrypt \
	  --with-mysql=mysqlnd \
	  --with-mysqli=mysqlnd \
	  --with-pdo-mysql=mysqlnd \
	  --enable-mbstring

	make
	sudo make install

## Configure Apache

### Edit httpd.conf:
	<IfModule dir_module>
	    DirectoryIndex index.html index.php
	</IfModule>

	<IfModule php5_module>
	    AddType application/x-httpd-php .php
	</IfModule>

### enable virtual hosts:

BASH:

	mkdir /usr/local/apache2/conf/sites

In httpd.conf:

	NameVirtualHost *:80
	Include conf/sites

Base virtualhost file (conf/sites/localhost):

	<VirtualHost *:80>
	    ServerName localhost
	    DocumentRoot /Users/andrew/Sites/localhost

	    <Directory /Users/andrew/Sites/localhost>
	        Options +FollowSymLinks
	        AllowOverride All
			Order allow,deny
			Allow from all
	    </Directory>

	</VirtualHost>




[0]: http://sourceforge.net/projects/mcrypt/files
[1]: http://www.ijg.org
[2]: http://freetype.sourceforge.net/index2.html
[3]: http://www.libpng.org/pub/png/libpng.html