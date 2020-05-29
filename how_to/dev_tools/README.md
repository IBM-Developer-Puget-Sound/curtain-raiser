# Install essential packages for devops

* __Git__ - for software configuration management [:link:](https://git-scm.com/)
* __Tmux__ - terminal multiplexing [:link:](https://github.com/tmux/tmux)
* __Curl__ - transfer data to or from server [:link:](http://manpages.ubuntu.com/manpages/bionic/man1/curl.1.html)
* __Less__ - view file pager [:link:](https://manpages.ubuntu.com/manpages/bionic/en/man1/less.1.html)
* __Docker Engine CE__ -  container daemon [:link:](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
* IBM Cloud CLI [:link:](https://github.com/IBM-Cloud/ibm-cloud-cli-release) __s390x NOT SUPPORTED__ 
  * cannot consider s390x as an enviroment that can be used to access other parts of the IBM Cloud


## Update and upgrade

```bash
sudo apt update --fix-missing
sudo apt upgrade
```

## Install the packages

```bash
sudo apt install git tmux curl less
```

## Install Docker

1. Check prerequisites

* Check Ubuntu version, then compare to Docker [requirements](https://docs.docker.com/install/linux/docker-ce/ubuntu/#os-requirements)
```bash
lsb_release -a
# one possible result something like
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 18.04.4 LTS
Release:        18.04
Codename:       bionic
```

2. Uninstall old versions [:link:](https://docs.docker.com/install/linux/docker-ce/ubuntu/#uninstall-old-versions)

```bash
sudo apt remove docker-ce docker-compose containerd
```

3. Install Docker Engine - Community [:link:](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-engine---community-1)

* package updates
```bash
sudo apt update
sudo apt upgrade -y
sudo apt clean
sudo apt autoremove
```

```bash
sudo apt install apt-transport-https \
                 ca-certificates \
                 curl \
                 gnupg-agent \
                 software-properties-common

sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=s390x] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

sudo apt update
sudo apt upgrade -y
```

* check the repository for available docker packages, excluding golang
  unless you want that.

```bash
sudo apt-cache search docker | grep -E "docker-ce*" | grep -Ev "golang*" | less
```

* install
```bash
sudo apt install docker-ce docker-compose
```

* test
```bash
sudo docker -v
sudo docker --help
sudo docker info
sudo docker run hello-world
```

## Reference

* apt-cache [:link:](http://manpages.ubuntu.com/manpages/bionic/man8/apt-cache.8.html)

* apt [:link:](https://www.debian.org/doc/manuals/debian-handbook/sect.apt-get.en.html)

* help ubuntu repositories command line [:link:](https://help.ubuntu.com/community/Repositories/CommandLine)

* Unix Stack Exchange issue 363048 [:link:](https://unix.stackexchange.com/questions/363048/unable-to-locate-package-docker-ce-on-a-64bit-ubuntu) 

* Youtube

   * IBM Developer Puget Sound 
     * tutorial [:link:](https://youtu.be/hcbuZ234SOg)
     * playlist [:link:](https://www.youtube.com/playlist?list=PL-j7VyctKguuCO8WkzaYauh4NosbtGLC_)

* Documentation
  - Ubuntu `apt` [:link:](https://help.ubuntu.com/lts/serverguide/apt.html)
  - Debian `apt` [:link:](https://www.debian.org/doc/manuals/debian-handbook/sect.apt-get.en.html)
