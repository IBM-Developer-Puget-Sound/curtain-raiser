# ssh-keygen

## Connecting to your IBM server instance will be done by secure shell; [ssh](https://en.wikipedia.org/wiki/Secure_Shell) .

### If you need or want to use a new authentication key pair for SSH, 
then run the ssh-keygen tool from the [command line](https://en.wikipedia.org/wiki/Command-line_interface). [[1]](https://cloud.ibm.com/docs/services/hp-virtual-servers?topic=hp-virtual-servers-generate_ssh#generating_ssh_command)

How do I know if my key is already available?
 ```bash
# Lists the files in your .ssh directory, if they exist
ls -al ~/.ssh
# display existing key files something like
# id_rsa
# id_rsa.pub
# /known_hosts
 ```

On your personal computer _only_ generate one ssh key per user. 
If you already have a key do not make another.  Copy this same 
key to several clients under the same users control in the same 
organization.  For example homeDesktop1, workDesktop2, workLaptop 
could all have the same copied key for the same user.  This single 
key will allow you to gain access to your remote server from 
several of your personal computers.

  * To generate a new private-public key pair from the bash command prompt:
    ```bash
    ssh-keygen \
    -t rsa \
    -b 4096 \
    -C "put myScreenName at myOrganization here" \
    -N "remember-this-super-secret-passphrase"

    # written as a single line command without the backslashes \
    ssh-keygen -t rsa -b 4096 -C "put myScreenName at myOrganization here" -N "remember-this-super-secret-passphrase"

    ```

  * The resulting keys will be stored in 

      `~/.ssh/id_rsa` # private key, not to be shared with anyone.

      `~/.ssh/id_rsa.pub` # public key

  * View the keys
    ```bash
    cat ~/.ssh/id_rsa
    cat ~/.ssh/id_rsa.pub
    ```

  * If the comment in the private key needs to be updated:
    ```bash
    ssh-keygen -o -c -C "myScreenName at myOrganization" -f ~/.ssh/id_rsa
    # Key now has comment '(null)'
    # The comment in your key file has been changed.
    ```
----

### Reference

1. ssh-keygen
   
   a. IBM cloud docs [:link:](https://cloud.ibm.com/docs/services/hp-virtual-servers?topic=hp-virtual-servers-generate_ssh)
  
   b. ssh . com [:link:](https://www.ssh.com/ssh/keygen)

   c. man ssh-keygen [Ubuntu](http://manpages.ubuntu.com/manpages/eoan/man1/ssh-keygen.1.html)

2. [SSH](https://en.wikipedia.org/wiki/Secure_Shell)
    
    a. Article: Getting started with SSH security ( developer.ibm [:link](https://developer.ibm.com/articles/au-sshsecurity/) )

    b. man ssh [man7](http://man7.org/linux/man-pages/man1/ssh.1.html)

    c. man ssh [die](https://linux.die.net/man/1/ssh)

3. [OpenSSH](https://en.wikipedia.org/wiki/OpenSSH)
    
    a. [openssh.com](https://www.openssh.com/)


    d. Ubuntu docs [openssh](https://help.ubuntu.com/lts/serverguide/openssh-server.html)

    e. Fedora docs f31 [openssh](https://docs.fedoraproject.org/en-US/fedora/f31/system-administrators-guide/infrastructure-services/OpenSSH/)