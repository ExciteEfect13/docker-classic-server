# WowStack: Vanilla WoW in Docker FAQ

This document covers frequently asked questions.

**Q: What is the purpose of WowStack?**

**A:** Seeing how available solutions for enjoying Vanilla WoW have pretty much
stagnated or are being more or less 3rd class citizens, we decided it was time
to start from scratch. So, we rebuild both the game engine but also the content
from scratch. As can be seen in this Docker runtime, we provide a database which
was rebuilt from scratch instead of being a backport based on TBC/WotLK data.

**Q: What version of MaNGOS/CMaNGOS is this?**

**A:** WowStack started in 2014 as a fork on [MaNGOS Zero][mangos-zero] to which
the founder of WowStack heavily contributed but since then has been combined
with changes from [CMaNGOS][cmangos-classic] and [TrinityCore][trinity-wotlk].

**Q: What are some of the key differences?**

**A:** The WowStack server has undergone a heavy remake after the official
release of the C++11, C++14 and C++17 standards. Most of the core frameworks has
been swapped out with modern code, lots of the usual segmentation faults have
been resolved. Apart from being rather stable, WowStack includes e.g.:

- full support for cheat detection via Warden
- user facing features such as
    - character name validation using the original rules for Vanilla WoW
    - working lag compensation
- and removal of all features which were not part of Vanilla Wow such as
  cross-faction communication, grouping, etc.
- improved use of original client data for data validation

**Q: How do I log in to the realm?**

**A:**: by default the system comes with a set of default accounts to demo all
available access levels:

The provided users are

- `ADMINISTRATOR` with password `ADMINISTRATOR`
- `GAMEMASTER` with password `GAMEMASTER`
- `MODERATOR` with password `MODERATOR`
- `PLAYER` with password `PLAYER`

**Q: How do I configure IP addresses?**

**A:** Currently you can provide IP addesses for login and world server. Using
`WOWSTACK_AUTH_BIND_IP` for the login server and `WOWSTACK_WORLD_BIND_IP` for
the world server, you should supply an IP address that is reachable either on
your host only or on your network if you want other players to connect.

**Q: Will you release the sources?**

**A:** The source code is licensed under the terms of the GNU AGPL 3.0 and will
be available on [Github][wowstack-classic-server].

**Q: Can I join the team?**

**A:** We're always interested in growing the team. If you are familiar with
MaNGOS/CMaNGOS/Trinity and consider yourself fairly driven and a little on the
crazy side, shoot an [email to us](mailto:support+team@wowstack.io).

[mangos-zero]: https://github.com/mangoszero/server
[cmangos-classic]: https://github.com/cmangos/mangos-classic
[trinity-wotlk]: https://github.com/TrinityCore/TrinityCore/tree/3.3.5
[wowstack-classic-server]: https://github.com/wowstack/classic-server
