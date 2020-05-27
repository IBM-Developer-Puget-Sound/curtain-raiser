### Add a user
> where `myusername` is replaced with the
> actual user screen name

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

