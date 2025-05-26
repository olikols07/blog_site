# Raspberry pi imager guide

## Setup in Raspberry Pi Imager
Select the PI device you are going to use
in my case that i the Raspberry PI 4.
We want to use a server version of the os so i choose the "Raspberry Pi OS (Other)" alternative and choose Raspberry Pi OS Lite for a basic instalation
and then select the correct sd card

After that you can select the advanced options, here you can set the hostname, enable ssh, set the username and password and configure the locale settings.
After that you can click on write and wait for the process to finish.

## connecting to the Raspberry Pi

After the process is finished, you can insert the SD card into your Raspberry Pi and power it on.
You can now connect to your Raspberry Pi using ssh with the hostname you set or the IP address assigned by your router.
If you used a ssh key, you can connect using the key instead of the password.