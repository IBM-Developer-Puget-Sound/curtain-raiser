# Jitsi Meet [:link:](https://jitsi.org/jitsi-meet/)
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
sudo apt install apt-transport-https
sudo apt update
sudo apt -y install jitsi-meet
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
> In case jitsi-meet is no longer needed

* permanently remove the jitsi packages. :warning: Current users will be unceremoniously dropped.

```bash
sudo apt remove --purge \
     jigasi jitsi-meet jitsi-meet-web-config \
     jitsi-meet-prosody jitsi-meet-turnserver \
     jitsi-meet-web jicofo jitsi-videobridge2
```

* close the previously opened ports
```bash
# delete accept
sudo iptables -D INPUT -p tcp -m tcp --dport 80 -j ACCEPT
sudo iptables -D INPUT -p tcp -m tcp --dport 443 -j ACCEPT
sudo iptables -D INPUT -p udp -m udp --dport 10000 -j ACCEPT

# add reject
iptables -A INPUT -p tcp --dport 80 -j REJECT
iptables -A INPUT -p tcp --dport 443 -j REJECT
iptables -A INPUT -p udp --dport 10000 -j REJECT

iptables -S   # list rules in chain
iptables -nvL # list all the rules
```

* remove hidden configuration files
```bash
sudo rm -rf ~/.jitsi-meet-cfg/
```

* remove the jitsi gpg key
```bash
sudo apt-key list | less
# choose the Jitsi hash last eight characters
sudo apt-key remove NNNNnnnn
```
* remove the source list
```bash
rm /etc/apt/sources.list.d/jitsi-stable.list
```

## Reference

* ubuntu iptables manpage [:link:](http://manpages.ubuntu.com/manpages/bionic/en/man8/iptables.8.html)

* ubuntu apt-key manpage [:link:](http://manpages.ubuntu.com/manpages/bionic/en/man8/apt-key.8.html)
