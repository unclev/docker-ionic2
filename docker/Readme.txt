Modify or create the files according to your needs:

.env IONIC_BRANCH ionic version to start a projects. Defautls to 2. May be 1. Eg.:
IONIC_BRANCH=1

docker-compose.yml may contain PUID and PGID arguments reptesent ionicuser uid and gid within the image.

Create a shell alias for quick launch ...
alias ionic=docker-compose run --rm --service-ports dev ionic'

Installed the following packages:
--> Ubuntu 16.04, with curl
--> Nodejs version 7.x, git
--> NPM install globally ionic, cordova, typescript, gulp

NOTE: Do not run npm update -g npm ... reinstalling npm v3 fails on Docker