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
docker container rm hello-world(NAMES) \
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
mkdir ~/workspace
cd ~/workspace
sudo rm -rf docker-jitsi-meet
```

## Quick start docker-jitsi-meet [:link:](https://github.com/jitsi/docker-jitsi-meet/blob/master/README.md#quick-start)

> will this docker image  work on architecture s390x ?
> [no](https://forums.docker.com/t/standard-init-linux-go-190-exec-user-process-caused-exec-format-error/49368/5) because "You have to run the docker image
> that was built for a particular Architecture on a
> docker node that is running that same Architecture."

```bash
cd ~/workspace

git clone https://github.com/jitsi/docker-jitsi-meet && cd docker-jitsi-meet

cp env.example .env

./gen-passwords.sh

mkdir -p ~/.jitsi-meet-cfg/{web/letsencrypt,transcripts,prosody,jicofo,jvb,jigasi,jibri}

docker-compose up -d

```

## Visit your newly installed and running jitsi-meet server

`https://ip.adddress.here:8443`

