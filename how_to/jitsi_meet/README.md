# Jitsi Meet
> on IBM s390x

## Prerequisites
Make sure you already have an [ssh-key](https://github.com/IBM-Developer-Puget-Sound/curtain-raiser/blob/master/how_to/ssh/keygen/README.md), HPV [server](https://github.com/IBM-Developer-Puget-Sound/curtain-raiser/blob/master/how_to/hp_virtual_server/README.md), essential devops [packages](https://github.com/IBM-Developer-Puget-Sound/curtain-raiser/blob/master/how_to/dev_tools/README.md), and limited [access](https://github.com/IBM-Developer-Puget-Sound/curtain-raiser/blob/master/how_to/fail2ban/README.md).

## Quick install [:link:](https://github.com/jitsi/jitsi-meet/blob/master/doc/quick-install.md#jitsi-meet-quick-install)

```bash
sudo echo 'deb https://download.jitsi.org stable/' >> /etc/apt/sources.list.d/jitsi-stable.list

sudo curl -so -  https://download.jitsi.org/jitsi-key.gpg.key | sudo apt-key add -

# OR
#sudo wget -qO -  https://download.jitsi.org/jitsi-key.gpg.key | sudo apt-key add -
```

## Open ports in your firewall
```bash
sudo iptables -nvL # list open ports
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
sudo iptables -A INPUT -p udp --dport 10000 -j ACCEPT
```

## Install jitsi meet [:link:](https://github.com/jitsi/jitsi-meet/blob/master/doc/quick-install.md#install-jitsi-meet)

```bash
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get -y install jitsi-meet
```

## Generate a Let's Encrypt certificate [:link:](https://github.com/jitsi/jitsi-meet/blob/master/doc/quick-install.md#generate-a-lets-encrypt-certificate-optional-recommended)
* ONLY FOR fully qualified domain names like `https://mywebsite.com`
  * do NOT do this if you will be testing with the IP address
```bash
/usr/share/jitsi-meet/scripts/install-letsencrypt-cert.sh
```

## Test the installation [:link:](https://github.com/jitsi/jitsi-meet/blob/master/doc/quick-install.md#confirm-that-your-installation-is-working)
```
https://my.ip.address
# OR
https://rtc-meet.mywebsite.com
```

## Remove [:link:](https://github.com/jitsi/jitsi-meet/blob/master/doc/quick-install.md#uninstall)
* permanently remove the jitsi packages. :warning: Current users will be unceremoniously dropped.

```bash
sudo apt-get purge jigasi jitsi-meet jitsi-meet-web-config \
              jitsi-meet-prosody jitsi-meet-turnserver \
              jitsi-meet-web jicofo jitsi-videobridge2
```

* close the previously opened ports
```bash

```


## Reference

* ubuntu iptables manpage [:link:](http://manpages.ubuntu.com/manpages/bionic/en/man8/iptables.8.html)

