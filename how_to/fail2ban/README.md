# Fail2ban limits failed login attempts

> Once the server is powered on there will be
> unauthorized attempts to ssh login by hackers
> from around the world. Ban attempted logins
> from the hackers IP address for some time.

```bash
# which can be inspected with
tail /var/log/auth.log # OR
cat /var/log/auth.log | more

# OR with specific error messages like
grep "Connection closed by" /var/log/auth.log | more

grep "Disconnected from invalid user" /var/log/auth.log | more

grep "Received disconnect from" /var/log/auth.log | more
# etc
```

## Prerequisite

These instructions apply to the following:
```bash
uname -o # operating-system
# GNU/Linux
uname -v # kernel-version
# #69-Ubuntu SMP Wed Sep 4 20:55:38 UTC 2019
uname -i # hardware-platform
# s390x

sudo apt update && apt upgrade -y
python3 --version
# if python3 not already installed, then
sudo apt install -y python3

# know your ssh port
sudo grep Port /etc/ssh/sshd_config
```

## Install ( on Ubuntu )

The instructions suggest

```bash
sudo apt install -y fail2ban
sudo fail2ban-client --version
# Fail2Ban v0.10.2-2
# Compare to latest version on github

# check status
systemctl status fail2ban
```
however, if the OS packaged version is not
the latest desired then try uninstalling
the older version and cloning the latest
version from github.

```bash
sudo apt uninstall fail2ban
git clone https://github.com/fail2ban/fail2ban.git
cd fail2ban
sudo python setup.py install
sudo fail2ban-client --version
```

## Configure
```bash
# copy
sudo cp /etc/fail2ban/fail2ban.conf /etc/fail2ban/fail2ban.local
# just to see the file is there
sudo cat /etc/fail2ban/fail2ban.local | more
```

## Configure jail.local
```bash
# copy
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
vim /etc/fail2ban/jail.local
```
* vim help [:link:](https://vimhelp.org/)
  * `i` insert mode
  * `esc` exit insert mode
  * `:` `w` `enter` write to file
  * `:` `q` `enter` quit editing

In file `jail.local` confirm/edit the following:

```bash
# Whitelist your IP for example
#ignoreip = 127.0.0.1/8 ::1

# "bantime" is the number of seconds that a host is banned.
# 24 hours x 60 minutes = 1440 minutes
bantime  = 1440m

# A host is banned if it has generated "maxretry" 
# during the last "findtime" seconds.
findtime  = 10m

# "maxretry" is the number of failures before a 
# host gets banned.
maxretry = 3

# JAILS
# SSH servers
[sshd] # <- this is the name of the jail!
enabled = true # add this line
```

## Start, enable and check status
```bash
sudo systemctl start fail2ban
sudo systemctl enable fail2ban
# check status
sudo systemctl status fail2ban
```

## Attempt a hack on server under test

* With an IP address different from your local IP 

  a. log into a remote server

  b. from the remote server

     * with a fake user name attempt to ssh
       into the server under test

```bash
ssh goodusername@remote.server.ip
# from within that server
ssh whitehat@server.under.test
# view the jailed IP addresses
```


## View the jailed IP addresses
After attackers have made their attempted login
their IP addresses will appear in the log.

```bash
sudo fail2ban-client status sshd # in jail sshd
Status for the jail: sshd
|- Filter
|  |- Currently failed:	0
|  |- Total failed:	0
|  `- File list:	/var/log/auth.log
`- Actions
   |- Currently banned:	0
   |- Total banned:	0
   `- Banned IP list:
```
__OR__

```bash
sudo cat /var/log/fail2ban.log | more
```

## Additional help
```bash
sudo fail2ban-client --help
```

## Stopping
```bash
# stop all jails and terminate server
sudo fail2ban-client stop
```

## Reference

* Fail2ban main-page [:link:](https://www.fail2ban.org/wiki/index.php/Main_Page)
* Wikipedia [:link:](https://en.wikipedia.org/wiki/Fail2ban)
* Github [:link:](https://github.com/fail2ban/fail2ban)
* Tecmint article [:link:](https://www.tecmint.com/use-fail2ban-to-secure-linux-server/)

* Youtube
  - IBM Developer Puget Sound 
    * tutorial [:link:](https://youtu.be/Wh5kpnsZg84)
    * playlist [:link:](https://www.youtube.com/playlist?list=PL-j7VyctKguuCO8WkzaYauh4NosbtGLC_)

* Documentation
  - Ubuntu `apt` [:link:](https://help.ubuntu.com/lts/serverguide/apt.html)
  - Debian `apt` [:link:](https://www.debian.org/doc/manuals/debian-handbook/sect.apt-get.en.html)
