# SSH

Connecting to your IBM server instance will be done by secure shell; [ssh](https://en.wikipedia.org/wiki/Secure_Shell) .

### ssh-keygen

If you need or want to use a new authentication key pair for SSH, run the ssh-keygen tool from the command line. [[1]](https://cloud.ibm.com/docs/services/hp-virtual-servers?topic=hp-virtual-servers-generate_ssh#generating_ssh_command)

On your personal computer _only_ generate one ssh key per user. If you already have a key do not make another.  Copy this same key to several clients under the same users control in the same organization.  For example homeDesktop1, workDesktop2, workLaptop could all have the same copied key for the same user.

  * To generate a new key pair from the bash command prompt:
    ```bash
    ssh-keygen \
    -t ras \
    -b 4096 \
    -C "put myScreenName at myOrganization here" \
    -N "remember-this-superSecret-passphrase"

    # written as a single line command without the backslashes \
    ssh-keygen -t ras -b 4096 -C "put myScreenName at myOrganization here" -N "remember-this-superSecret-passphrase"

    ```

  * The resulting keys will be stored in 

      `~/.ssh/id_rsa` # private key

      `~/.ssh/id_rsa.pub` # public key

  * If the comment in the private key needs to be updated
    ```bash
    ssh-keygen -o -c -C "myScreenName at myOrganization" -f ~/.ssh/id_rsa
    # Key now has comment '(null)'
    # The comment in your key file has been changed.
    ```
----

### Reference

1. IBM cloud docs [ssh-keygen](https://cloud.ibm.com/docs/services/hp-virtual-servers?topic=hp-virtual-servers-generate_ssh)

2. [SSH](https://en.wikipedia.org/wiki/Secure_Shell)
    
    a. man ssh [man7](http://man7.org/linux/man-pages/man1/ssh.1.html)

    b. man ssh [die](https://linux.die.net/man/1/ssh)

    c. Article: Getting started with SSH security ( developer.ibm [:link](https://developer.ibm.com/articles/au-sshsecurity/) )

3. [OpenSSH](https://en.wikipedia.org/wiki/OpenSSH)
    
    a. [openssh.com](https://www.openssh.com/)


    d. Ubuntu docs [openssh](https://help.ubuntu.com/lts/serverguide/openssh-server.html)

    e. Fedora docs f31 [openssh](https://docs.fedoraproject.org/en-US/fedora/f31/system-administrators-guide/infrastructure-services/OpenSSH/)