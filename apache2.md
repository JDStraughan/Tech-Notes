# Apache 2



## Configure and build, install

BASH:

	./configure \
	  --prefix=/usr/local/apache2 \
	  --enable-so --enable-mods-shared=all \
	  --with-mpm=prefork \
	  --with-included-apr \
	  --with-ssl=/usr \
	  --enable-ssl
	
	make
	sudo make install

## Launchd (OS X)

Create file: /LibraryLaunchDaemons/com.apache.apachectl.plist

XML:

	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
	<plist version="1.0">
	<dict>
	    <key>Label</key>
	    <string>com.apache.apachectl</string>
	    <key>ProgramArguments</key>
	    <array>
	        <string>/usr/local/apache2/bin/apachectl</string>
	        <string>start</string>
	    </array>
	    <key>RunAtLoad</key>
	    <true/>
	</dict>
	</plist>