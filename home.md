<!-- TITLE: Home -->
<!-- SUBTITLE: A quick summary of Home -->

# Header

# Favanet Services
## Non - /opt/

### Home Assistant

For controlling the home

Port 8123

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

### Plex
For movies, tv shows, images, recordings, music.
Port 32400

`docker run -d --name plex --network=host -e TZ="America/Denver" -v /opt/plex/config:/config -v /mnt/md0/public/Movies:/data/Movies -v /mnt/md0/public/TV:/data/TV -v /mnt/md0/public/Music:/data/Music -v /mnt/md0/public/Images:/data/Images -p 32400:32400 plexinc/pms-docker`

### Couchpotato
For downloading Movies
Port 5050

### Snipe
For tracking all inventory in the house
Port 81

Also has a mysql db running on Port 32768

