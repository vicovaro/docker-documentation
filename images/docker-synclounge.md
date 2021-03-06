# [linuxserver/synclounge](https://github.com/linuxserver/docker-synclounge)

[![GitHub Stars](https://img.shields.io/github/stars/linuxserver/docker-synclounge.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&logo=github)](https://github.com/linuxserver/docker-synclounge)
[![GitHub Release](https://img.shields.io/github/release/linuxserver/docker-synclounge.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&logo=github)](https://github.com/linuxserver/docker-synclounge/releases)
[![GitHub Package Repository](https://img.shields.io/static/v1.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=linuxserver.io&message=GitHub%20Package&logo=github)](https://github.com/linuxserver/docker-synclounge/packages)
[![GitLab Container Registry](https://img.shields.io/static/v1.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=linuxserver.io&message=GitLab%20Registry&logo=gitlab)](https://gitlab.com/Linuxserver.io/docker-synclounge/container_registry)
[![MicroBadger Layers](https://img.shields.io/microbadger/layers/linuxserver/synclounge.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge)](https://microbadger.com/images/linuxserver/synclounge "Get your own version badge on microbadger.com")
[![Docker Pulls](https://img.shields.io/docker/pulls/linuxserver/synclounge.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=pulls&logo=docker)](https://hub.docker.com/r/linuxserver/synclounge)
[![Docker Stars](https://img.shields.io/docker/stars/linuxserver/synclounge.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=stars&logo=docker)](https://hub.docker.com/r/linuxserver/synclounge)
[![Jenkins Build](https://img.shields.io/jenkins/build?labelColor=555555&logoColor=ffffff&style=for-the-badge&jobUrl=https%3A%2F%2Fci.linuxserver.io%2Fjob%2FDocker-Pipeline-Builders%2Fjob%2Fdocker-synclounge%2Fjob%2Fmaster%2F&logo=jenkins)](https://ci.linuxserver.io/job/Docker-Pipeline-Builders/job/docker-synclounge/job/master/)
[![LSIO CI](https://img.shields.io/badge/dynamic/yaml?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=CI&query=CI&url=https%3A%2F%2Flsio-ci.ams3.digitaloceanspaces.com%2Flinuxserver%2Fsynclounge%2Flatest%2Fci-status.yml)](https://lsio-ci.ams3.digitaloceanspaces.com/linuxserver/synclounge/latest/index.html)

[Synclounge](https://github.com/samcm/synclounge) is a third party tool that allows you to watch Plex in sync with your friends/family, wherever you are.

## Supported Architectures

Our images support multiple architectures such as `x86-64`, `arm64` and `armhf`. We utilise the docker manifest for multi-platform awareness. More information is available from docker [here](https://github.com/docker/distribution/blob/master/docs/spec/manifest-v2-2.md#manifest-list) and our announcement [here](https://blog.linuxserver.io/2019/02/21/the-lsio-pipeline-project/).

Simply pulling `linuxserver/synclounge` should retrieve the correct image for your arch, but you can also pull specific arch images via tags.

The architectures supported by this image are:

| Architecture | Tag |
| :----: | --- |
| x86-64 | amd64-latest |
| arm64 | arm64v8-latest |
| armhf | arm32v7-latest |


## Usage

Here are some example snippets to help you get started creating a container from this image.

### docker

```
docker create \
  --name=synclounge \
  -e TZ=Europe/London \
  -e EXTERNAL_URL=your.domain.com \
  -e EXTERNAL_SERVER_PORT=80 `#optional` \
  -e AUTH_LIST=plexuser1,plexuser2,email1,machineid1 `#optional` \
  -e AUTOJOIN_ENABLED=false `#optional` \
  -e AUTOJOIN_ROOM=roomname `#optional` \
  -e AUTOJOIN_PASSWORD=password `#optional` \
  -p 8088:8088 \
  -p 8089:8089 \
  --restart unless-stopped \
  linuxserver/synclounge
```


### docker-compose

Compatible with docker-compose v2 schemas.

```yaml
---
version: "2.1"
services:
  synclounge:
    image: linuxserver/synclounge
    container_name: synclounge
    environment:
      - TZ=Europe/London
      - EXTERNAL_URL=your.domain.com
      - EXTERNAL_SERVER_PORT=80 #optional
      - AUTH_LIST=plexuser1,plexuser2,email1,machineid1 #optional
      - AUTOJOIN_ENABLED=false #optional
      - AUTOJOIN_ROOM=roomname #optional
      - AUTOJOIN_PASSWORD=password #optional
    ports:
      - 8088:8088
      - 8089:8089
    restart: unless-stopped
```

## Parameters

Docker images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

### Ports (`-p`)

| Parameter | Function |
| :----: | --- |
| `8088` | Web app port |
| `8089` | Server port |


### Environment Variables (`-e`)

| Env | Function |
| :----: | --- |
| `TZ=Europe/London` | Specify a timezone to use EG Europe/London |
| `EXTERNAL_URL=your.domain.com` | The webapp and the server will be accessible at this address via reverse proxy (alternatively, you can define an external IP address). |
| `EXTERNAL_SERVER_PORT=80` | If you're not using a reverse proxy, you can define the external port for the server here. |
| `AUTH_LIST=plexuser1,plexuser2,email1,machineid1` | If set, only the users defined here and the users of the plex servers defined here will be able to access the server. Use e-mails, plex usernames and/or plex server machine ids, comma separated, no spaces. |
| `AUTOJOIN_ENABLED=false` | Set to `true` to let users autojoin the server and a room (specified by the `AUTOJOIN_ROOM` var). |
| `AUTOJOIN_ROOM=roomname` | Set the room name for auto joining (requires `AUTOJOIN_ENABLED` set to `true`). |
| `AUTOJOIN_PASSWORD=password` | Set the password for the room for auto joining (requires `AUTOJOIN_ENABLED` set to `true`). |

### Volume Mappings (`-v`)

| Volume | Function |
| :----: | --- |



## Environment variables from files (Docker secrets)

You can set any environment variable from a file by using a special prepend `FILE__`.

As an example:

```
-e FILE__PASSWORD=/run/secrets/mysecretpassword
```

Will set the environment variable `PASSWORD` based on the contents of the `/run/secrets/mysecretpassword` file.

## Umask for running applications

For all of our images we provide the ability to override the default umask settings for services started within the containers using the optional `-e UMASK=022` setting.
Keep in mind umask is not chmod it subtracts from permissions based on it's value it does not add. Please read up [here](https://en.wikipedia.org/wiki/Umask) before asking for support.


## Application Setup

The web app is accessible at `http://SERVERIP:8088`. The server by default is available at `http://SERVERIP:EXTERNAL_SERVER_PORT/slserver`.

Note: The server address is hardcoded to `http` as `https` is not recommended due to not working with external plex clients. When you reverse proxy, use `http` as the external proto for both webapp and server.


## Docker Mods
[![Docker Mods](https://img.shields.io/badge/dynamic/yaml?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=mods&query=%24.mods%5B%27synclounge%27%5D.mod_count&url=https%3A%2F%2Fraw.githubusercontent.com%2Flinuxserver%2Fdocker-mods%2Fmaster%2Fmod-list.yml)](https://mods.linuxserver.io/?mod=synclounge "view available mods for this container.")

We publish various [Docker Mods](https://github.com/linuxserver/docker-mods) to enable additional functionality within the containers. The list of Mods available for this image (if any) can be accessed via the dynamic badge above.


## Support Info

* Shell access whilst the container is running:
  * `docker exec -it synclounge /bin/bash`
* To monitor the logs of the container in realtime:
  * `docker logs -f synclounge`
* Container version number
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' synclounge`
* Image version number
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' linuxserver/synclounge`

## Versions

* **01.06.20:** - Rebasing to alpine 3.12.
* **05.11.20:** - Intial Release.
