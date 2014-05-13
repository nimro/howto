# Set Keyboard Layout - aerosaur

The default keyboard layout (used for the shell) is set by 4 lines in the file /etc/default/keyboard, 
which looks like this:

	XKBMODEL="pc105"
	XKBLAYOUT="gb"
	XKBVARIANT=""
	XKBOPTIONS=""

The above means the computer is configured for a standard 105-key keyboard, UK layout. However,
this doesn't take care of variant such as the mac keyboard. You can find a list of available
parameters for the above file by reading the console setup utility:

	cat /usr/share/console-setup/KeyboardNames.pl | less

This will give you a great long list of things; a set of models, layouts, variants and options,
such as:

	'gb' => {
	        'English (UK, Colemak)' => 'colemak',
	        'English (UK, Dvorak with UK punctuation)' => 'dvorakukp',
 	        'English (UK, Dvorak)' => 'dvorak',
        	'English (UK, Macintosh international)' => 'mac_intl',
        	'English (UK, Macintosh)' => 'mac',
        	'English (UK, extended WinKeys)' => 'extd',
        	'English (UK, international with dead keys)' => 'intl',
	},

Which means to choose, for example, the UK Macintosh variant we choose the key 'mac' - i.e. 

	XKBVARIANT="mac"
