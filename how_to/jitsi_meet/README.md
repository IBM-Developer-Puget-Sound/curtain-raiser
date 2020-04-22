# Jitsi Meet quick install [:link:](https://github.com/jitsi/jitsi-meet/blob/master/doc/quick-install.md#jitsi-meet-quick-install)
> on IBM s390x

```bash
echo 'deb https://download.jitsi.org stable/' >> /etc/apt/sources.list.d/jitsi-stable.list

curl -so -  https://download.jitsi.org/jitsi-key.gpg.key | sudo apt-key add -

# OR
#wget -qO -  https://download.jitsi.org/jitsi-key.gpg.key | sudo apt-key add -
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
apt-get install apt-transport-https
apt-get update
apt-get -y install jitsi-meet
```

## Generate a Let's Encrypt certificate [:link:](https://github.com/jitsi/jitsi-meet/blob/master/doc/quick-install.md#generate-a-lets-encrypt-certificate-optional-recommended)

```bash
/usr/share/jitsi-meet/scripts/install-letsencrypt-cert.sh
```
