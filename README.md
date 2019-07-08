# sttyfix utility

This is a Python written utility that fixes the stty size for serial console to
the actual window size. The default stty size on serial console is only 24x80.
When executing vi, less, or other commands the display outputs text in a small
24x80 fragment of your terminal window. This utulity fixes it.

## How to use it.

Usually when using the serial console you set up a new system without network
connectivity yet.  In this case you should use a serial connection to transfer
this utility to new system.  However, it is common that many distros have no
X|Y|Z-modem or kermit utilities. In this case, the simplest method to transfer
the utlity is to copy-paste to the console.

Run this

	$ cat << EOF | sudo tee /usr/local/bin/sttyfix > /dev/null
	-- this is the copy-pasted sttyfix utility body --
	$ EOF
	$ sudo chmod a+x /usr/local/bin/sttyfix

Check the result

	$ stty size
	$ sttyfix
	$ stty size

To fix stty size permanently on booting add these lines to /etc/profile

	if [[ $(ps -o 'tty=' -p $$) =~ "ttyS" ]] ; then
	    /usr/local/bin/sttyfix
	fi
