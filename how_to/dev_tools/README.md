# Install essential packages for devops

* __Git__ - for software configuration management [:link:](https://git-scm.com/)
* __Tmux__ - terminal multiplexing [:link:](https://github.com/tmux/tmux)
* __Curl__ - transfer data to or from server [:link:](http://manpages.ubuntu.com/manpages/bionic/man1/curl.1.html)
* __Less__ - view file pager [:link:](https://manpages.ubuntu.com/manpages/bionic/en/man1/less.1.html)
* __Docker Engine CE__ -  container daemon [:link:](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
* IBM Cloud CLI [:link:](https://github.com/IBM-Cloud/ibm-cloud-cli-release) __s390x NOT SUPPORTED__ 
  * cannot consider s390x as an enviroment that can be used to access other parts of the IBM Cloud

## Prerequisites
* Check Ubuntu version, then compare to Docker [requirements](https://docs.docker.com/install/linux/docker-ce/ubuntu/#os-requirements)
```bash
lsb_release -a
# one possible result
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 18.04.4 LTS
Release:	18.04
Codename:	bionic
```

## Install the packages

```bash
sudo apt --yes --force-yes install git tmux curl less
```

## Install Docker

1. Uninstall old versions [:link:](https://docs.docker.com/install/linux/docker-ce/ubuntu/#uninstall-old-versions)
2. Install Docker Engine - Community [:link:](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-engine---community)
```bash
```
