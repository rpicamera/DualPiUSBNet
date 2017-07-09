# DualPiUSBNet
Dual raspberry pi system communicate via USB Ethernet.  
Master Raspberry Pi: any type of Raspberry Pi
Slave Raspberry Pi: mode A only.

##  Set slave rpi as usb gadget. 
Follow the this instruction http://blog.gbaman.info/?p=791. In short, here is the steps copied from that instruction. 

_For this method, alongside your Pi Zero, MicroUSB cable and MicroSD card, only an additional computer is required, which can be running Windows (with Bonjour, iTunes or Quicktime installed), Mac OS or Linux (with Avahi Daemon installed, for example Ubuntu has it built in)._

1. _Flash Raspbian Jessie full or Raspbian Jessie Lite onto the SD card_

2. _Once Raspbian is flashed, open up the boot partition (in Windows Explorer, Finder etc) and add to the bottom of the config.txt file dtoverlay=dwc2 on a new line, then save the file._

3. _If using a recent release of Jessie (Dec 2016 onwards), then create a new file simply called ssh in the SD card as well. By default SSH is now disabled so this is required to enable it. Remember - Make sure your file doesn't have an extension (like .txt etc)!_

4. _Finally, open up the cmdline.txt. Be careful with this file, it is very picky with its formatting! Each parameter is seperated by a single space (it does not use newlines). Insert modules-load=dwc2,g_ether after rootwait. To compare, an edited version of the cmdline.txt file at the time of writing, can be found here._

5. _That's it, eject the SD card from your computer, put it in your Raspberry Pi Zero and connect it via USB to your computer. It will take up to 90s to boot up (shorter on subsequent boots). It should then appear as a USB Ethernet device. You can SSH into it using raspberrypi.local as the address._

##  Change the master network interface. 

In this step, we are going to set the master pi as USB master and test the connection with the slave pi. Add the following line at the end of the file /etc/network/interfaces

---
allow-hotplug usb0

mapping hotplug

        script grep
        
        map usb0

iface usb0 inet static

       address 192.168.2.14
       
       netmask 255.255.255.0
       
       broadcast 192.168.2.255
       
       up iptables -I INPUT 1 -s 192.168.2.15 -j ACCEPT
       
---
       
Reboot the mater pi, connect slave pi to the master pi's USB 0. Login to the master pi, try to ping raspberrypi.local, if it shown the ip address begin with 169, then it means master pi was set up successfully. I haven't figure it out how to share the internet with the slave pi. So, if needed update, upgrade or install any software, you need to connect the slave pi to the PC or Mac with internet share on. 
