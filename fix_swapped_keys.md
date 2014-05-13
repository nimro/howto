Fix swapped keys on your UK Macintosh Keyboard
==============================================

This fixes the problem where a UK Macintosh keyboard would have the correct layout except
the `/~ and §/± keys would be swapped.

Temporarily
-----------

The following command will have immediate effect, but rebooting will reset the configuration:

$ echo 0 | sudo tee /sys/module/hid_apple/parameters/iso_layout

(The meaning of fnmode values is as described in the preceding section.)

Permanently
-----------

1. Append the configuration line to the file /etc/modprobe.d/hid_apple.conf creating it if necessary:

$ echo options hid_apple iso_layout=0 | sudo tee -a /etc/modprobe.d/hid_apple.conf

2. Trigger copying the configuration into the initramfs bootfile.

$ sudo update-initramfs -u -k all

3. Optionally, reboot

$ sudo reboot
