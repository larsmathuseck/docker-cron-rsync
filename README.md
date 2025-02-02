# Docker cron rsync [Fork from https://github.com/Glideh/docker-cron-rsync]

## Usage

Example with a `docker-compose.yml`:

```yml
version: "3"

services:
  rsync:
    image: larsmathuseck/cron-rsync:latest
    volumes:
      - ~/.ssh:/host-ssh:ro
      - ./backup:/backup
    environment:
      RSYNC_CRONTAB: "* * * * *"
      RSYNC_OPTIONS: "-tv toto@example.com:backup/*.tgz /backup"
```

Here we want to synchronize (download new files) from a remote server with rsync by SSH every minute.

Every minute this will be executed:

```bash
rsync -tv toto@example.com:backup/*.tgz /backup
```

## Concept

The aim is to be able to mirror files (ie. backups) with a minimal installation required (only Docker)  
The image is less than 4MB.

In order to synchronize files, rsync is included in the image.  
Remote host rsyncs are also possible with the included SSH client.

Host SSH keys are used simply by mounting them in the container `~/.ssh:/host-ssh:ro`.
