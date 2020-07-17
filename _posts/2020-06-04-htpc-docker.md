---
layout: post
title: HTPC
cover-img: /assets/img/docker.png
thumbnail-img: /assets/img/docker.png
tags: [Docker, HTPC]
comments: false
published: true
---

## HTPC {#HTPC}
I have been using Kodi for many years now on various setups along the years. Generally I have all my Media library (TV Shows, Movies, Music etc) on a Ubuntu server and on each TV I have either another PC or a Android box running Kodi to access all my media.

I have been testing with Jellyfin for my LG SmartTV's and I think when the WebOS app is ready I will switch to it instead of Kodi. Time will tell...

This post is how I am currently setting up the HTPC server it might change or be updated over time.  

---

### Update and Upgrade
<p>After installing Ubuntu server I like to run update and upgrade before starting to install anything:</p>
~~~
  sudo apt-get update && sudo apt-get upgrade -y
~~~

If it's the first time generally takes awhile to complete.  

### SSH and remote connection
After that's done I can begin installing SSH to I can do everything over my network:
```
sudo apt-get install openssh-server
```

Then I test if it's working and move on to my PC, most of the times I'm using Ubuntu so I just fire up the terminal with `Ctrl+Alt+T` and ssh into it, if by any nonsence I'm using Windows generally I use Putty.

### Environment Variables
For things like usernames, passwords, emails, folder locations and things that I have to repeatedly type in I like to use environment variables to do so I edit the file `/etc/environment` with:
~~~
sudo nano /etc/environment
~~~   
  
And at the bottom of the file I start writing all my variables

_Example:_
~~~
SERVERIP=""
DOCKERUSER=""
TZ=""

USERDIR=""
DOCKERDIR=""
SHAREDDIR=""
DOWNLOADSDIR=""
MEDIADIR=""
TVSHOWSDIR=""
MOVIESDIR=""
MUSICDIR=""

USERNAME=""
PASSWORD=""
EMAIL=""
SQL_ROOT_PW=""
~~~
  
Add or remove and complete the variables. Save and reboot the HTPC with

### Installing Docker
Installing Docker is pretty straight forward and it's basically a copy/paste of a couple of command lines:
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt update
```

Then you do:
```
apt-cache policy docker-ce
``` 

and it should output some versions table etc.
Instaling Docker can be done with:
```
sudo apt install docker-ce
```

And then install Docker-compose,

### Docker Without Sudo
To avoid needing to use sudo before docker commands I had my username to docker group with:
```
sudo usermod -aG docker ${USER}
```

Reboot and it's done!

### Docker Containers
I came to noticed I use a lot of [Linuxserver](https://hub.docker.com/u/linuxserver/) containers they are very easy to configure and use with lots of examples and explanations.

Currently these are the containers I'm using.

| NAME          | DESCRIPTION                                 |
| ------------- | ------------------------------------------- |
| bazarr        | Downloads Subtitles                         |
| ha-dockermon  | Gives HA access to Docker containers        |
| jackett       | ProxyServer for Radarr, Sonarr and Lidarr   |
| jellyfin      | Media Player System                         |
| letsencrypt   | Nginx and Let's Encrypt for HTTPs           |
| lidarr        | Music Media                                 |
| ouroboros     | Keeps Docker containers updated             |
| qbittorrent   | Torrents Downloader                         |
| radarr        | Movies Media                                |
| sonarr        | TV Shows Media                              |

and after it's complete create all the necessaries folders for the docker containers.

~~~
mkdir -p ~/docker
cd ~/docker
touch docker-compose.yml
mkdir -p portainer qbittorrent radarr sonarr bazarr jackett ha_dockermon
~~~


* Create and edit docker-compose    
_Example:_

{% highlight yaml %}
version: "3.7"

networks:
  HTPC:
    external:
      name: HTPC
  default:
    driver: bridge

services:
  portainer:
    image: portainer/portainer:latest
    container_name: portainer
    hostname: portainer
    networks:
      - HTPC
    restart: always
    command: -H unix:///var/run/docker.sock
    ports:
      - "${SERVERIP}:9000:9000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ${DOCKERDIR}/portainer:/data
      - ${SHAREDDIR}:/shared
    environment:
      - TZ=${TZ}
{% endhighlight %}
