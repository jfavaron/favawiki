<!-- TITLE: Home -->
<!-- SUBTITLE: A quick summary of Home -->

# Header

Wiki has its own repo, so it's in a separate location.

`~/wiki`

There are some files that need to be in `~/wiki` that we're going to backup in the other repo for containers.

`config.yml`
`docker-compose.yml`

If you have those two files in `~/wiki` and still have all of the markdown files on github, then issuing a `sudo docker-compose up` should do the trick.

Should never have to manually set up or lose data on the Wiki again. Also the files are now portable to other systems (or just readable via git....)

https://github.com/jfavaron/favawiki