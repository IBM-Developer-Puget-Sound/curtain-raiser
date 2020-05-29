### Add a user [:link:]()
> where `myusername` is replaced with the
> actual user screen name

#### Prerequisite
1. Provision a Hyper Protect Virtual Server [:link:](../hp_virtual_server/README.md)
----


```bash
# logged in as root (or sudoer)
adduser myusername
cd /home/myusername

mkdir .ssh
chmod 700 .ssh
chown myusername:myusername .ssh
cd .ssh

touch authorized_keys
chmod 600 authorized_keys
chown myusername:myusername authorized_keys

# copy and paste the contents of public key
# id_rsa.pub for `myusername` into the file
#  authorized_keys, save and quit
vim authorized_keys
exit

# request the new user attempt a login
ssh myusername@the.system.ip
```

### Add user to sudoers list
```bash
usermod -aG sudo myusername
#check it
groups myusername
```

### Delete a user

```bash
# remove user from sudoers list
usermod -G "" myusername

#check it
groups myusername

# remove user any
deluser myusername

# remove users home directory
rm -rf /home/myusername

# check user list that user is removed
compgen -u
```

### Reference
* Ubuntu
  * `adduser` [:link:](http://manpages.ubuntu.com/manpages/bionic/en/man8/adduser.8.html)
  * `usermod` [:link:](http://manpages.ubuntu.com/manpages/bionic/en/man8/usermod.8.html)
  * `groups` [:link:](http://manpages.ubuntu.com/manpages/bionic/en/man1/groups.1.html)
  * `deluser` [:link:](http://manpages.ubuntu.com/manpages/bionic/en/man8/deluser.8.html)
* GNU
  * `compgen` [:link:](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins.html)

* Youtube
  * IBM Developer Puget Sound
    * this tutorial [:link:](https://www.youtube.com/watch?v=j-fvecza1tM)
    * playlist [:link:](https://www.youtube.com/playlist?list=PL-j7VyctKguuCO8WkzaYauh4NosbtGLC_)
