# WowStack: a dockerized Vanilla WoW environment

**WARNING**: this is a work in progress environment and _may_ fail to work.

Running [Vanilla Wow][wow-1] can be quite the drag if compiling and maintaining
a moving Open Source project is not your forté.

Now things are easier. This provides a containerized environment for running
a full environment supporting Vanilla WoW, and allows enjoying a long-gone game
of World of Warcraft using client 1.12.x (in your prefered locale).

## TODO: Work in progress

- [ ] Extract required data from Vanilla Wow game client on startup

See **notes** below for manual map extraction!

## DONE: Work completed

- [x] Provision and configure MariaDB
- [x] Provision Vanilla WoW authentication server
- [x] Configure authentication server on startup
- [x] Provision authentication database on startup
- [x] Provision Vanilla WoW game world server
- [x] Configure game world server on startup
- [x] Provision game world database on startup
- [x] Provision character database on startup

## Docker images

All Docker images are available on the Docker Hub, and updated frequently.

- [Map tools](https://hub.docker.com/r/wowstack/map-tools/)
- [Authentication server](https://hub.docker.com/r/wowstack/auth-server/)
- [Game World server](https://hub.docker.com/r/wowstack/world-server/)

Since this is a work in progress project, we highly recommend to frequently
run `docker-compose pull` before running the containers (at least weekly).

## Requirements

Since this is all prebuilt and updated by us, all you have to worry about is
having [Docker][docker] and [Docker Compose][docker-compose] installed.

Feel free to use Docker for Mac OS, Docker for Windows or Docker for Linux,
all work the same.

## Usage

First - to reduce initial start times - pull all Docker containers required by
executing:

```bash
docker-compose pull
```

This will retrieve the WowStack containers for map data, the authentication
server, and the game world server. To support this, we will also pull a MariaDB
container to house the game content during runtime.

As with any composed Docker environment, running the Vanilla WoW environment is
simple:

```bash
docker-compose up -d
```

When shutting down the containers, we recommend to also prune any created
volumes, as this avoids issues with importing the base data into MariaDB:

```bash
docker-compose down
docker volume prune -f
```

## Extracting Vanilla WoW client data manually

**Take note** to a few things here:

- `-v $HOME/Applications/World\ of\ Warcraft:/opt/wowstack/data` is passed on to
  supply the container with the Vanilla World of Warcraft game installation. Pass
  in the _base_ directory, e.g. `C:/World\ of\ Warcraft` or `$HOME/WoW-enGB`
- ```-v `pwd`/data/wowstack:/opt/wowstack/share``` is passed in as output directory
  for generated files. This directory is then mounted to the world server.

### Camera, DBC and map files extraction

```bash
$ docker run \
    -e WOWSTACK_APP_NAME=classic-server \
    -v $HOME/Applications/World\ of\ Warcraft:/opt/wowstack/data \
    -v `pwd`/data/wowstack:/opt/wowstack/share \
    -it \
    --rm wowstack/map-tools:latest \
    sh -c '/opt/wowstack/bin/map-extractor --help'
```

### Height map files extraction

```bash
$ docker run \
    -e WOWSTACK_APP_NAME=classic-server \
    -v $HOME/Applications/World\ of\ Warcraft:/opt/wowstack/data \
    -v `pwd`/data/wowstack:/opt/wowstack/share \
    -it \
    --rm wowstack/map-tools:latest \
    sh -c '/opt/wowstack/bin/vmap-extractor --help'
```

### Height map files assembly

```bash
$ docker run \
    -e WOWSTACK_APP_NAME=classic-server \
    -v $HOME/Applications/World\ of\ Warcraft:/opt/wowstack/data \
    -v `pwd`/data/wowstack:/opt/wowstack/share \
    -it \
    --rm wowstack/map-tools:latest \
    sh -c '/opt/wowstack/bin/vmap-assembler --help'
```

### Movement map generation

```bash
$ docker run \
    -e WOWSTACK_APP_NAME=classic-server \
    -v $HOME/Applications/World\ of\ Warcraft:/opt/wowstack/data \
    -v `pwd`/data/wowstack:/opt/wowstack/share \
    -it \
    --rm wowstack/map-tools:latest \
    sh -c '/opt/wowstack/bin/mmap-generator --help'
```

[wow-1]: http://blizzard.com/games/wow/
[docker]: https://docs.docker.com/install/
[docker-compose]: https://docs.docker.com/compose/install/
