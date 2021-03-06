How to seamlessly connect device on a linux/Windows dual boot system. -SRE
==========================================================================

source: <a>http://ubuntuforums.org/showthread.php?t=1479056&p=9363229#post9363229</a>

***

Find the bluetooth address of the PC/dongle (let's say AA:11:11:11:11:11).
Find the bluetooth address of the keyboard (let's say BB:22:22:22:22:22).
Pair the device normally, under Linux (via the Gnome panel).

There should be a file called <code>/var/lib/bluetooth/AA:11:11:11:11:11/linkkeys</code>, which contains a line like this:

	BB:22:22:22:22:22 xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx 0 6

Here, xxx...x is 16 bytes written continuously in hexadecimal, that's the link key.

Pair the device normally, under Windows (this will change the key). Get the key from Windows. E.g. in this registry entry:

	SYSTEM\ControlSet002\services\BTHPORT\Parameters\Keys\aa1111111111\bb2222222222

Unfortunately, RegEdit will probably say "access is denied" when Keys is reached, even when logged on as administrator.

Reboot under Linux, install chntpw.


To avoid unwanted modifications of the Windows registry from Linux, it may be preferable to copy the SYSTEM file somewhere else, from: <code>/path/to/Windows/System32/config/SYSTEM</code>
Open it with chntpw (browse registry with ls/cd; help with ?):

	chntpw -e SYSTEM
	ls
	cd ControlSet001\Services\BTHPORT\Parameters\Keys
	ls
	cd aa1111111111
	ls
	hex bb2222222222

This produces something like this:

	:00000 xx xx xx xx xx xx xx xx xx xx xx xx xx xx xx xx 

Here, "xx xx ... xx" is another 16 bytes, in hexadecimal, represented the link key set up in Windows. There will possibly be other characters after the 16 bytes; only copy the first 16 bytes (16 pairs after :00000).

Finally, copy that (and remove the spaces) to replace the value already in <code>/var/lib/bluetooth/AA:11:11:11:11:11/linkkeys</code>.

Disconnect / reconnect device via bluetooth applet.
