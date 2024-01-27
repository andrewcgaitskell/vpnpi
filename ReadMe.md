# Introduction

Install and get noip working on your chosen port

# Installing noip 

https://docs.pivpn.io/guides/dynamic-dns/

https://medium.com/enekochan/compile-install-configure-and-make-start-on-boot-the-noip-com-client-in-raspbian-30e2dbf8910d

https://www.noip.com/support/knowledgebase/running-linux-duc-v3-0-startup-2

# install noip

## Download and Install

        wget http://www.noip.com/client/linux/noip-duc-linux.tar.gz
        tar xzvpf noip-duc-linux.tar.gz
        cd `find . -name "noip-[0-9]*"`
        sudo make
        sudo make install

## Configure ??

        sudo /usr/local/bin/noip2 -C


        

# Ensuring noip starts / restarts on reboot

If you want to run the client at boot time (which you’ll probably want…) create an init.d script file called /etc/init.d/noip2 with this content:

        #! /bin/sh

        ### BEGIN INIT INFO
        # Provides:          noip2
        # Required-Start:    $syslog
        # Required-Stop:     $syslog
        # Default-Start:     2 3 4 5
        # Default-Stop:      0 1 6
        # Short-Description: noip.com client service
        ### END INIT INFO
        
        # . /lib/lsb/init-functions
        case "$1" in
            start)
                echo "Starting noip2."
                /usr/local/bin/noip2
            ;;
            stop)
                echo "Shutting down noip2."
                killall noip2
                #killproc /usr/local/bin/noip2
            ;;
            *)
                echo "Usage: $0 {start|stop}"
                exit 1
        esac
        
        exit 0

Then give it executable permissions and update the rc.d scripts:

        sudo chmod +x /etc/init.d/noip2
        sudo update-rc.d noip2 defaults

# Installation of openvpn using pivpn script

https://www.pcmag.com/how-to/how-to-create-a-vpn-server-with-raspberry-pi

https://www.pivpn.io/

    curl -L https://install.pivpn.io | bash

The answers should be the defaults throughout.

# Setting up 

# Copy the file from the pi to the host

scp pi@192.168.1.999:/home/vpnpi/ovpns/vpn.ovpn .

## parallel running on port 1195

fix internal ip address of pi

login to your router and port forward your chosen port.

Install openvpn using the script above.

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
    
    and create a new .ovpn file that worked on new port


# Firewalla

https://help.firewalla.com/hc/en-us/community/posts/360005828413-Change-OpenVPN-port-

# Checking the logs on the pi

sudo journalctl -u openvpn

## shows the service starting and stopping

grep VPN /var/log/syslog

#

# setupVars.conf

                PLAT=Raspbian
                OSCN=bullseye
                USING_UFW=0
                pivpnforceipv6route=0
                IPv4dev=eth0
                IPv4addr=192.168.1.xx/24
                IPv4gw=192.168.1.1
                install_user=vpnpi
                install_home=/home/vpnpi
                VPN=openvpn
                pivpnPROTO=udp
                pivpnPORT=119X
                pivpnDNS1=10.44.176.1
                pivpnDNS2=
                pivpnSEARCHDOMAIN=
                pivpnHOST=blahblah.ddns.net
                TWO_POINT_FOUR=1
                pivpnENCRYPT=256
                USE_PREDEFINED_DH_PARAM=
                INPUT_CHAIN_EDITED=0
                FORWARD_CHAIN_EDITED=0
                INPUT_CHAIN_EDITEDv6=
                FORWARD_CHAIN_EDITEDv6=
                pivpnDEV=tun0
                pivpnNET=10.44.176.0
subnetClass=24
pivpnenableipv6=0
ALLOWED_IPS=""
UNATTUPG=1
INSTALLED_PACKAGES=(unattended-upgrades)
HELP_SHOWN=1
