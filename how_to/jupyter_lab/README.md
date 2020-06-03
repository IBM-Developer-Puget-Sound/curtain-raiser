## Serve Jupyter Lab for a single user

### Prerequisites
1. Provision a Hyper Protect Virtual Server [:link:](../hp_virtual_server/README.md)
2. Add sudoer user (ie not root) [:link:](../add_user/README.md)
3. Install python3, pip3 and venv [:link:](../install_python/README.md)
----

### Install Jupyter Lab with pip
> login as the sudoer user

```bash
sudo apt install jupyter-notebook # required to run lab
mkdir myjupyterlab
mkdir ./myjupyterlab/mynotebooks
python3 -m venv ~/myjupyterlab --prompt myjupyter

# start the virtual environment

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
sudo iptables -A INPUT -p tcp --dport 8888 -j ACCEPT
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
where nnn.nnn.nnn is the IP address of the server

### Persist Jupyter Lab as a daemon

* create a file in $HOME
```bash
#!/bin/sh
# file: jupyterlab.sh
# Starts the Jupyter notebook server on port 8888
# called by the file /etc/systemd/system/jupyterlab.service
# Expect this file to be set to executable
#  with command `chmod +x jupyterlab.sh`
cd ~/myjupyterlab/mynotebooks
startJupyter="jupyter lab --ip=0.0.0.0 --port=8888 --no-browser"
echo "$startJupyter"
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
sudo systemctl enable jupyterlab.service
sudo service jupyterlab start
sudo service jupyterlab status

### Test availability of the service
Enter into web browser URL bar
```bash
# if password has been set
http://nnn.nnn.nnn:8888
```

### Uninstall
> If no longer needed, removes all related packages

* stop virtual environment
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
```

### TODO
* TLS not set up yet, communication over insecure connection
* NodeJS is expected to be on server for managing javascript extensions

### Reference

* Jupyter Lab readthedocs [:link:](https://jupyterlab.readthedocs.io/en/stable/)
* Persist Jupyer Lab as a service notes from aiafterwork [:link:](https://www.aiafterwork.com/running-jupyterlab-on-ubuntu-startup/)
* systemd directives [:link:](https://www.freedesktop.org/software/systemd/man/systemd.directives.html)
