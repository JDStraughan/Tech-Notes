# Modifying the bash include path

On OS X (or Linux, for that matter), the easiest way to get bash to prefer your custom 
compiled applications is to modify your path to prefer /usr/local/bin (or whatever you 
use) over /usr/bin, etc...

It's pretty easy. Just create ~/.bash_login if it doesn't already exist, and add the following lines:

	PATH="/usr/local/bin:/usr/local/sbin:$PATH"
	export PATH

The ":" is the path separator.

Adding $PATH to the end of the new path variable appends the global path to the end of your custom one.