## Docker installation

This is a simple guide on how to install docker on a raspberry pi

Make sure you have sudo access to the PI!!

To install docker itself i recommed using the 
<a href="https://docs.docker.com/engine/install/">documentation from docker</a> the documentation has a convenience script seen bellow

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
```

Then you need to allow your user to use docker commands without sudo


```
sudo usermod -aG docker $USER
```

And then instaid of rebooting we reload the changes

```
newgrp docker
```

## Example containers and configuration

In my opinion the best way to do docker compose files is a structure like this

/docker/[Projectname]/compose.yml
 
so we create the docker directory, allow the user to read and write in the directory and also creating a symbolic link to the directory in the home directory 

```
sudo mkdir /docker
sudo chown $USER:$USER /docker
sudo ln -s /docker
```

# Creating a pihole installation

folowing the structure we make a new directory in /docker

```
mkdir /docker/pihole
cd /docker/pihole
nano compose.yml
```

then copy the pihole example compose file from below
```
# More info at https://github.com/pi-hole/docker-pi-hole/ and https://docs.pi-hole.net/
services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    ports:
      # DNS ports
      - "53:53/tcp"
      - "53:53/udp"
      # WEB GUI
      - "80:80/tcp"
      - "443:443/tcp"
      # DHCP
      - "67:67/udp"
    environment:
      TZ: 'Europe/Oslo'
      FTLCONF_webserver_api_password: '(change me)'
      FTLCONF_dns_listeningMode: 'all'
    volumes:
      - './etc-pihole:/etc/pihole'
    cap_add:
      - NET_ADMIN
      - SYS_TIME
      - SYS_NICE
    restart: unless-stopped
```

Save and exit and now we are ready to start pihole with

```
docker compose up -d
```