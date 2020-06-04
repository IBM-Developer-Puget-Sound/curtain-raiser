## Install python and pip
> Python should already be installed with `update` and `upgrade` commands,

> however Pip is not automatically installed

### Prerequisites
1. Provision a Hyper Protect Virtual Server [:link:](../hp_virtual_server/README.md)
2. Add sudoer user (ie not root) [:link:](../add_user/README.md)
----

```bash
# check if python already installed
p3=$(python3 --version)
substring=$(echo $p3 | cut -b 1-8)
if [ $substring != "Python 3" ]
then
  # go ahead with install
  sudo apt install python3
else
  echo "$p3 already installed"
fi

# # # #

# check if pip already installed
p3=$(pip3 --version)
substring=$(echo $p3 | cut -b 1-3)
if [ $substring != "pip" ]
then
  # go ahead with install
  sudo apt install python3-pip
else
  echo "$p3 already installed"
fi
```

### Install the virtual environment
```bash
sudo apt install python3-venv
```

### Reference
* virtual environment [:link:](https://docs.python.org/3/tutorial/venv.html#virtual-environments-and-packages)
