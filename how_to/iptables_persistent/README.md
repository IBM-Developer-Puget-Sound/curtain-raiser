## Persist iptables

### Prerequisites
1. Provision a Hyper Protect Virtual Server [:link:](../hp_virtual_server/README.md)
2. Add sudoer user (ie not root) [:link:](../add_user/README.md)
3. Install essential packages for devops [:link:](../dev_tools/READ.me)

### Install
```bash
sudo apt install iptables-persistent
```
> command also installs `netfilter-persistent`

### Usage
```bash
sudo netfilter-persistent --help
# /usr/sbin/netfilter-persistent (start|stop|restart|reload|flush|save)
```
* command accesses the files at `/etc/iptables/rules*` and then
  automatically loads `/etc/iptables/rules`  during boot

### Reference
* Ubuntu
  * iptables howto [:link:](https://help.ubuntu.com/community/IptablesHowTo)
  * netfilter-persistent [:link:](http://manpages.ubuntu.com/manpages/bionic/man8/netfilter-persistent.8.html)
