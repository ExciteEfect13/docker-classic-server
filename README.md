# WowStack: a container-based Vanilla WoW environment

Running [Vanilla Wow][wow-1] can be quite the drag if compiling and maintaining
a moving Open Source project is not your forté.

Now things are easier. This provides a containerized environment for running
a full environment supporting Vanilla WoW, and allows enjoying a long-gone game
of World of Warcraft using client 1.12.x (in your prefered locale).

We now have a [FAQ](FAQ.md) up, answering some of the questions we received.

## Support

Meanwhile we are on [Discord][discord], so come chat with us.

Like our work and want to show appreciation? Give the repository a star, visit
our [Patreon][patreon] and become an supporter. :heart_eyes:

## Requirements

Since this is all prebuilt and updated by us, all you have to worry about is
having [Docker][docker] and [Docker Compose][docker-compose] installed.

Feel free to use Docker for Mac OS, Docker for Windows or Docker for Linux,
all work the same.

- A Docker CE/EE runtime, version 18.02 or newer
- Docker Compose, version 1.24.0 or newer

## Usage

Copy `.env.dist` to `.env` and cutomize the settings to your liking or leave
them as is for default behaviour.

To reduce initial start times  pull all Docker containers required by executing:

```console
docker-compose pull
```

This will retrieve the WowStack containers for map data, the authentication
server, and the game world server. To support this, we will also pull a MariaDB
container to house the game content during runtime.

As with any composed Docker environment, running the Vanilla WoW environment is
simple:

```console
docker-compose up -d
```

When shutting down the containers, we recommend to also prune any created
volumes, as this avoids issues with importing the base data into MariaDB:

```console
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

```console
$ docker run \
    --name wow_map_generation \
    -e WOWSTACK_FORCE_REBUILD=no \
    -v $HOME/Applications/World\ of\ Warcraft:/opt/wowstack/data \
    -v `pwd`/data/wowstack:/opt/wowstack/share \
    -d wowstack/map-tools:latest
```

This process might take a few hours to complete. Setting `WOWSTACK_FORCE_REBUILD`
to `yes` will trigger regeneration of all data even if there already are files
from previous runs.

## Docker images

All Docker images are available on the Docker Hub, and updated frequently.

- [Map tools](https://hub.docker.com/r/wowstack/map-tools/)
- [Authentication server](https://hub.docker.com/r/wowstack/auth-server/)
- [Game World server](https://hub.docker.com/r/wowstack/world-server/)

Since this is a work in progress project, we highly recommend to frequently
run `docker-compose pull` before running the containers (at least weekly).

[docker]: https://docs.docker.com/install/
[docker-compose]: https://docs.docker.com/compose/install/

[wowstack]: https://wowstack.io/
[wow-1]: http://blizzard.com/games/wow/
[discord]: https://discord.gg/TttsRMp
[patreon]: https://www.patreon.com/bePatron?u=10897042
