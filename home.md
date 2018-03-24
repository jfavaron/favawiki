<!-- TITLE: Home -->
<!-- SUBTITLE: A quick summary of Home -->

# Header

# Favanet Services
## Non - /opt/

### Favawiki

Wiki has its own repo, so it's in a separate location.

`~/wiki`

There are some files that need to be in `~/wiki` that we're going to backup in the other repo for containers.

`config.yml`
`docker-compose.yml`

If you have those two files in `~/wiki` and still have all of the markdown files on github, then issuing a `sudo docker-compose up` should do the trick.

Should never have to manually set up or lose data on the Wiki again. Also the files are now portable to other systems (or just readable via git....)

https://github.com/jfavaron/favawiki

Has two separate containers, a mongo db and the main one. If needed, exec into the image and go use `cd /logs` to look at log outputs.

## /opt/

### Portainer
Meant for controlling all of the other docker containers.
Port 9000

`docker volume create portainer_data`
`docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v /opt/portainer:/data portainer/portainer`

### Plex
For movies, tv shows, images, recordings, music.
Port 32400

`docker run -d --name plex --network=host -e TZ="America/Denver" -v /opt/plex/config:/config -v /mnt/md0/public/Movies:/data/Movies -v /mnt/md0/public/TV:/data/TV -v /mnt/md0/public/Music:/data/Music -v /mnt/md0/public/Images:/data/Images -p 32400:32400 plexinc/pms-docker`

### Couchpotato
For downloading Movies
Port 5050

`docker create --name=couchpotato -p 5050:5050 -v /opt/couchpotato/config:/config -v /mnt/md0/public/tmp/:/downloads -v /mnt/md0/public/Movies/:/movies linuxserver/couchpotato`

### Snipe
For tracking all inventory in the house
Port 81

Also has a mysql db running on Port 32768

https://snipe-it.readme.io/docs/docker

First run MySQL for Snipe
`docker run --name snipe-mysql --env-file=/opt/snipeit/my_env_file.env -d -P mysql:5.6`

Then run the actual service
`docker run -d -p 81:80 --name="snipeit" --link snipe-mysql:mysql --env-file=/opt/snipeit/my_env_file.env snipe/snipe-it`

### Home Assistant
For controlling the home
Port 8123

`docker run -d --name="home-assistant" -v /opt/homeassistant:/config -v /etc/localtime:/etc/localtime:ro --net=host homeassistant/home-assistant`
