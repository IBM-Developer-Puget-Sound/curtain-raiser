# Installing Jitsi Meet with Docker [:link:](https://github.com/jitsi/docker-jitsi-meet/blob/master/README.md#jitsi-meet-on-docker)
> on IBM s390x

## Prerequisites
* Have installed
  * docker-ce
  * docker-compose

## Docker housekeeping
```bash
docker --help | less
docker container --help | less #and etc
```
* look to see what containers are available
  *  should be no containers for a fresh start
```bash
docker container ls --all # look to see if empty
```

* check to see if any running containers
```bash
docker-compose ps
```
* shutdown all currently running containers
```bash
docker-compose down
```

* remove the "old" containers
  * something like
```bash
docker container rm hello-world \
                    other-container-name-here
```

* remove unneeded images
```bash
docker images -a # list all the images
docker rmi IMAGE-ID-HERE
```

* start with an empty workspace
  *  by completely removing the the last revision
     * __THIS WILL DELETE EVERYTHING!__
```bash
cd ~/workspace
sudo rm -rf docker-jitsi-meeti
```

## Quick start [:link:](https://github.com/jitsi/docker-jitsi-meet/blob/master/README.md#quick-start)

```bash
cd ~/workspace

git clone https://github.com/jitsi/docker-jitsi-meet && cd docker-jitsi-meet
cp env.example .env
mkdir -p ~/.jitsi-meet-cfg/{web/letsencrypt,transcripts,prosody,jicofo,jvb,jigasi,jibri}
docker-compose up -d.

```

