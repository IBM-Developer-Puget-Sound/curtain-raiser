## Serve Jupyter Labs for a single user

### Prerequisites
1. Provision a Hyper Protect Virtual Server [:link:](../hp_virtual_server/README.md)
2. Add sudoer user (ie not root) [:link:](../add_user/README.md)
3. Install python3, pip3 and venv [:link:](../install_python/README.md)
----

### Install Jupyter Lab with pip
> login as the sudoer user

```bash
sudo apt install jupyter-notebook # required to run lab
#mkdir mynotebooks
mkdir myjupyterlab
mkdir ../myjupyterlab/mynotebooks
#python3 -m venv ~/mynotebooks --prompt myjupyter
python3 -m venv ~/myjupyterlab --prompt myjupyter
#cd mynotebooks 
cd myjupyterlab
#pip3 install jupyter       # required to run lab
pip3 install jupyterlab

```

### Add a password for Jupyter Lab


### Open port 8888
> This is the default Jupyter port
```bash
sudo iptables -A INPUT -p tcp --dport 8888 -j ACCEPT
```

### Activate Jupyter Lab temporarily
```bash
#sudo jupyter lab --ip=0.0.0.0  --no-browser --allow-root
jupyter lab --ip=0.0.0.0  --no-browser --allow-root
# which will present a typical path and token
```
### Test availability from a browser
Enter into URL bar of browser
```bash
http://nnn.nnn.nnn.nnn:8888/?token=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
where nnn.nnn.nnn.nnn is the IP address of the server

### Persist Jupyter Lab as a daemon


### Test availability of the process

### Uninstall
> If no longer needed

### Reference

* Jupyter Lab readthedocs [:link:](https://jupyterlab.readthedocs.io/en/stable/)

