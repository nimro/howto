## Handy Commands ##

# Fix broken kernel modules!
sudo /etc/init.d/vboxdrv setup

# Start a vm, headless with RDP
vboxheadless --startvm VMNAME

# Start a vm, headless with no RDP
vboxheadless --startvm VMNAME --vrde off

# Other power controls
vboxmanage controlvm VMNAME pause|resume|reset|poweroff|savestate|acpipowerbutton|acpisleepbutton

# Forward ports
### example: vboxmanage modifyvm virtualmachine1 --natpf1 "ssh,tcp,,2222,,22"
vboxmanage modifyvm VMNAME --natpf1 "PROTOCOL,tcp|udp,,FROMPORT,,TOPORT"

# Delete forwarded ports
vboxmanage modifyvm VMNAME --natpf1 delete "PROTOCOL"

## Initial Setup ##

# Create vm

cd <vm directory>
vboxmanage createvm --name <name> --register
vboxmanage createhd --filename HDDIMAGENAME.vdi --size 30000
vboxmanage storagectl VMNAME --name "IDE Controller" --add ide --controller PIIX4
vboxmanage storageattach VMNAME --storagectl "IDE Controller" --port 0 --device 0 --type hdd --medium HDDIMAGENAME.vdi

# Attach install media
vboxmanage storageattach VMNAME --storagectl "IDE Controller" --port 0 --device 1 --type dvddrive --medium /path/to/installer/image

# Set RAM, other setup
vboxmanage modifyvm VMNAME --memory 1024 --acpi on --boot1 dvd --nic1 nat

# Configure an RDP port and set RDP authentication.
### null will set no authentication. external will allow any user with an account on the host to use RDP with this VM
vboxmanage modifyvm VMNAME --vrdeport RDPPORT --vrdeauthtype null|external

## Housekeeping ##

# Once your Operating System is installed, shut down your VM
# Use this to remove the install media:
vboxmanage storageattach VMNAME --storagectl "IDE Controller" --port 0 --device 1 --type dvddrive --medium none

## Auto-start ##

# Every user who wants to enable autostart for individual machines has to set the path to # the autostart database directory:
VBoxManage setproperty autostartdbpath /etc/vbox

# Now we are ready to set the VM's we choose to start.
VBoxManage modifyvm VMNAME --autostart-enabled on
# This will create a myuserid.start file in /etc/vbox directory

