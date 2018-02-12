[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://github.com/linuxserver/Heimdall
[hub]: https://hub.docker.com/r/lsioarmhf/heimdall-aarch64/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/heimdall-aarch64
[![](https://images.microbadger.com/badges/version/lsioarmhf/heimdall-aarch64.svg)](https://microbadger.com/images/lsioarmhf/heimdall-aarch64 "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/heimdall-aarch64.svg)](http://microbadger.com/images/lsioarmhf/heimdall-aarch64 "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/heimdall-aarch64.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/heimdall-aarch64.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/arm64/arm64-heimdall)](https://ci.linuxserver.io/job/Docker-Builders/job/arm64/job/arm64-heimdall/)

Heimdall is a way to organise all those links to your most used web sites and web applications in a simple way.

Simplicity is the key to Heimdall.

Why not use it as your browser start page? It even has the ability to include a search bar using either Google, Bing or DuckDuckGo.

[![heimdall](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/heimdall-banner.png)][appurl]

## Usage

```
docker create \
--name=heimdall \
-v <path to data>:/config \
-e PGID=<gid> -e PUID=<uid>  \
-p 80:80 -p 443:443 \
-e TZ=<timezone> \
lsioarmhf/heimdall-aarch64
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 80` - The web-services.
* `-p 443` - The SSL-Based Webservice
* `-v /config` - Contains your www content and all relevant configuration files.
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` - timezone ie. `America/New_York`

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it heimdall /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application 

Access the web gui at http://SERVERIP:PORT

## Info

* To monitor the logs of the container in realtime `docker logs -f heimdall`.


* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' heimdall`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/heimdall-aarch64`

## Versions

+ **11.02.18:** Initial Release.
