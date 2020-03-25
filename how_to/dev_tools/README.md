# Install essential packages for devops

* Git for software configuration management [:link:](https://git-scm.com/)
* Tmux - terminal multiplexing [:link](https://github.com/tmux/tmux)
* Curl - transfer data to or from server [:link](http://manpages.ubuntu.com/manpages/bionic/man1/curl.1.html)
* Less - view file pager [:link](https://manpages.ubuntu.com/manpages/bionic/en/man1/less.1.html)
* Docker Engine CE -  container daemen [:link](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
* IBM Cloud CLI [:link](https://github.com/IBM-Cloud/ibm-cloud-cli-release) __s390x NOT SUPPORTED__ ( cannot consider s390x as a an enviroment that can be used to access other parts of the IBM Cloud )

## Prerequisites
* Check Ubuntu version, then compare to Docker requirements
```bash
lsb_release -a
# one possible result
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 18.04.4 LTS
Release:	18.04
Codename:	bionic
```
