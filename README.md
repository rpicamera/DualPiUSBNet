# DualPiUSBNet
Dual raspberry pi system communicate via USB Ethernet.  
Master Raspberry Pi: any type of Raspberry Pi
Slave Raspberry Pi: mode A only.

1.  set slave rpi as usb gadget. follow the this instruction http://blog.gbaman.info/?p=791. In short, here is the steps copied from that instruction. 
For this method, alongside your Pi Zero, MicroUSB cable and MicroSD card, only an additional computer is required, which can be running Windows (with Bonjour, iTunes or Quicktime installed), Mac OS or Linux (with Avahi Daemon installed, for example Ubuntu has it built in).
1.1. Flash Raspbian Jessie full or Raspbian Jessie Lite onto the SD card



1.2. Once Raspbian is flashed, open up the boot partition (in Windows Explorer, Finder etc) and add to the bottom of the config.txt file dtoverlay=dwc2 on a new line, then save the file.
1.3. If using a recent release of Jessie (Dec 2016 onwards), then create a new file simply called ssh in the SD card as well. By default SSH is now disabled so this is required to enable it. Remember - Make sure your file doesn't have an extension (like .txt etc)!
1.4. Finally, open up the cmdline.txt. Be careful with this file, it is very picky with its formatting! Each parameter is seperated by a single space (it does not use newlines). Insert modules-load=dwc2,g_ether after rootwait. To compare, an edited version of the cmdline.txt file at the time of writing, can be found here.
1.5. That's it, eject the SD card from your computer, put it in your Raspberry Pi Zero and connect it via USB to your computer. It will take up to 90s to boot up (shorter on subsequent boots). It should then appear as a USB Ethernet device. You can SSH into it using raspberrypi.local as the address.
2.  change the master network interface. Add the following line at the end of the file
