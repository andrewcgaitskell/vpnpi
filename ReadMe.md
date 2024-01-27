# Introduction

Install and get noip working on your chosen port

# Installing noip 

https://docs.pivpn.io/guides/dynamic-dns/

https://medium.com/enekochan/compile-install-configure-and-make-start-on-boot-the-noip-com-client-in-raspbian-30e2dbf8910d

https://www.noip.com/support/knowledgebase/running-linux-duc-v3-0-startup-2

# Installation of openvpn using pivpn script

https://www.pcmag.com/how-to/how-to-create-a-vpn-server-with-raspberry-pi

https://www.pivpn.io/

    curl -L https://install.pivpn.io | bash

The answers should be the defaults throughout.




# Setting up 

# Copy the file from the pi to the host

scp pi@192.168.1.999:/home/vpnpi/ovpns/vpn.ovpn .






## parallel running on port 1195

To point openvpn to a different port two changes need to be made.

Thank you to : https://github.com/pivpn/pivpn/issues/681#issuecomment-467276670

      sudo nano /etc/openvpn/server.conf
      change port and control + x to exit and save changes
      restart with "sudo reboot"

then

    type "sudo nano /etc/openvpn/easy-rsa/pki/Default.txt"
    edit the ip address and control + x to exit and save changes
    restart with "sudo reboot"

then

    pivpn add
    
    and create a new .ovpn file that worked on my new port -


# Firewalla

https://help.firewalla.com/hc/en-us/community/posts/360005828413-Change-OpenVPN-port-

# Checking the logs on the pi

sudo journalctl -u openvpn

## shows the service starting and stopping

grep VPN /var/log/syslog
