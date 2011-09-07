# MySQL

I don't really use this anymore. There isn't much advantage to compiling MySQL yourself, just use the binary.
But, just in case, here are instructions tested with 5.1 :)

## Configure the build, install
	
	./configure --prefix=/usr/local/mysql --enable-thread-safe-client --with-plugins=innobase
	make && make install

## Configure

### Data directory

BASH:
	cd /usr/local/mysql
	sudo ./bin/mysql_install_db --user=mysql
	sudo chown -R mysql ./var

### Launchd (OS X)

Create file: /Library/LaunchDaemons/com.mysql.mysqld.plist

XML:

	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
	<plist version="1.0">
	<dict>
	    <key>KeepAlive</key>
	    <true/>
	    <key>Label</key>
	    <string>com.mysql.mysqld</string>
	    <key>Program</key>
	    <string>/usr/local/mysql/bin/mysqld_safe</string>
	    <key>RunAtLoad</key>
	    <true/>
	    <key>UserName</key>
	    <string>mysql</string>
	    <key>WorkingDirectory</key>
	    <string>/usr/local/mysql</string>
	</dict>
	</plist>

Test launchd files with:

BASH:

	sudo launchctl load -w /Library/LaunchDaemons/com.mysql.mysqld.plist

### Test and create users

MYSQL:

	use mysql;
	select user, host, password from user; #see what's there
	delete from user where user = '';
	update user set password = password('password') where user = 'root';
	grant all on *.* to 'andrew'@'%' identified by 'password' with grant option;
	flush privileges;