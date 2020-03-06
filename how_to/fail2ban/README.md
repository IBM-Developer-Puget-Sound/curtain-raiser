# Fail2ban limits failed login attempts

> Once the server is powered on there will be
> unauthorized attempts to ssh login by hackers
> from around the world. Ban attempted logins
> from the hackers IP address for some time.

## Prerequisite
```bash
uname -or
sudo apt update && apt upgrade -y
python3 --version
sudo apt install -y python3 # if not alread installed
```

## Install
```bash
sudo apt install -y fail2ban
```

## Configure
```bash
sudo cp /etc/fail2ban/fail2ban.conf /etc/fail2ban/fail2ban.local
sudo cat fail2ban.local | less
```

## Configure jail.local
```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

## Start and Enable
```bash
sudo systemctl start fail2ban
sudo systemctl enable fail2ban
```

## View the jailed IP addresses
```bash
sudo fail2ban-client status sshd # for example
```

## Reference

* Fail2ban main-page [:link:](https://www.fail2ban.org/wiki/index.php/Main_Page)
* Wikipedia [:link:](https://en.wikipedia.org/wiki/Fail2ban)
* Github [:link:](https://github.com/fail2ban/fail2ban)
* Tecmint article [:link:](https://www.tecmint.com/use-fail2ban-to-secure-linux-server/)

* Youtube
  - IBM Developer Puget Sound 
    * tutorial [:link:]()
    * playlist [:link:](https://www.youtube.com/playlist?list=PL-j7VyctKguuCO8WkzaYauh4NosbtGLC_)
  - Eric lewis [:link:](https://youtu.be/Sm5XlFxWqdo)

* Documentation
  - Ubuntu `apt` [:link:](https://help.ubuntu.com/lts/serverguide/apt.html)
  - Debian `apt` [:link:](https://www.debian.org/doc/manuals/debian-handbook/sect.apt-get.en.html)
