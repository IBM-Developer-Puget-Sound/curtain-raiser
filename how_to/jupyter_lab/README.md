## Serve Jupyter Lab for a single user

### Prerequisites
1. Provision a Hyper Protect Virtual Server [:link:](../hp_virtual_server/README.md)
2. Add sudoer user (ie not root) [:link:](../add_user/README.md)
3. Install essential packages for devops [:link:](../dev_tools/READ.me)
4. Install `python3`, `pip3` and `venv` [:link:](../install_python/README.md)
5. Install `iptables-persistent` [:link:](../iptables_persistent/README.md)
----

### Install Jupyter Lab with pip
> login as the sudoer user

```bash
sudo apt install jupyter-notebook # required to run lab
mkdir myjupyterlab
mkdir ./myjupyterlab/mynotebooks

# create a virtual environmet
python3 -m venv ~/myjupyterlab --prompt myjupyter

# activate the virtual environment
source myjupyterlab/bin/activate

cd myjupyterlab
pip3 install jupyterlab

```

### Add a password for Jupyter Lab
* Automatic Password setup [:link:](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html#automatic-password-setup)
```bash
jupyter notebook password
```
__OR__

* Preparing a hashed password [:link:](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html#preparing-a-hashed-password)

### Open port 8888
> This is the default Jupyter port
```bash
# add a rule
sudo iptables -A INPUT -p tcp --dport 8888 -j ACCEPT
# make the iptables changes persistent after reboot
sudo iptables-save > /etc/iptables/rules.v4
```

### Activate Jupyter Lab temporarily
```bash
jupyter lab --ip=0.0.0.0  --no-browser
# which will present a typical path and token
# OR if password has been created, just the path
```
### Test availability from a browser
Enter into web browser URL bar
```bash
http://nnn.nnn.nnn:8888/?token=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
OR if password has been set
http://nnn.nnn.nnn:8888
```
> where nnn.nnn.nnn is the IP address of the server

> note this is not a secured connection ie __not__ https

### Persist Jupyter Lab as a service

* create a file in $HOME
```bash
#!/bin/sh
# filename: jupyterlab.sh
# Starts the Jupyter notebook server on port 8888
# called by the file /etc/systemd/system/jupyterlab.service
# Expect this file to be set to executable
#  with command `chmod +x jupyterlab.sh`
cd ~/myjupyterlab/mynotebooks
startJupyter="jupyter lab --ip=0.0.0.0 --port=8888 --no-browser"
logger "$startJupyter"
$startJupyter
```

* create a service file in directory `/etc/systemd/system/`
  * for example `sudo vim /etc/systemd/system/jupyterlab.service`
```bash
[Unit]
Description=JupyterLab
After=syslog.target network.target
[Service]
User=putmyusernamehere
ExecStart=/bin/bash /home/putmyusernamehere/jupyterlab.sh
[Install]
WantedBy=multi-user.target
```
### Start the service
```bash
sudo systemctl enable jupyterlab.service
sudo service jupyterlab start

# optionally
#   check the status
sudo service jupyterlab status

#   see log file entry
tail /var/log/syslog
```

### Test availability of the service
Enter into web browser URL bar
```bash
# if password has been set
http://nnn.nnn.nnn:8888
```
> may need to close and reopen browser to reset
> password cookies


### Reboot Server to re-test availability of service
```bash
sudo reboot
```
* Test availability of service as noted above

troubeshooting
* Confirm that the iptables have been reloaded
  with the port 8888 rule.
```bash
sudo iptables -S
```

### Uninstall
> If no longer needed, removes all related packages

* stop virtual environment
```bash
cd ~/myjupyterlab
deactivate
```

* remove virtual environment

```bash
pip3 uninstall jupyterlab
sudo apt remove --purge jupyter-notebook
rm -rf ~/jupyter_lab

# remove port 8888 from iptables
sudo iptables -D INPUT -p tcp -m tcp --dport 8888 -j ACCEPT
# list the rules
sudo iptables -S

# make sure hidden directory is removed
rm -rf ~/.jupyter

# remove start up scripts
rm ~/jupyterlab.sh
sudo rm /etc/systemd/system/jupyterlab.service

```

### TODO
* TLS not set up yet, communication over insecure connection
* NodeJS is expected to be on server for managing javascript extensions

### Reference

* Jupyter Lab readthedocs [:link:](https://jupyterlab.readthedocs.io/en/stable/)
* Persist Jupyer Lab as a service notes from aiafterwork [:link:](https://www.aiafterwork.com/running-jupyterlab-on-ubuntu-startup/)
* systemd directives [:link:](https://www.freedesktop.org/software/systemd/man/systemd.directives.html)

* Ubuntu
  * iptables how to [:link:](https://help.ubuntu.com/community/IptablesHowTo)
  * iptables-save [:link:](http://manpages.ubuntu.com/manpages/bionic/en/man8/iptables-save.8.html)
