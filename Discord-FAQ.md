**NOTE:** This is landing page for the `frequently-asked-questions` channel on [Discord](https://discord.gg/nSaXpCn), and as such mostly contains a collection of introductory links to other pages.

# Important links

## Basics

- [The actual FAQ page can be found here](https://github.com/cmangos/issues/wiki/FAQ-Frequently-Asked-Questions)  
- [Main wiki page](https://github.com/cmangos/issues/wiki)

Please refer to the main page and the side-bar for further general information about the project.

## Installation Instructions

- [Installation instructions for Windows/MacOS/Linux](https://github.com/cmangos/issues/wiki/Installation-Instructions)
- [Setting up a systemd service](https://github.com/cmangos/issues/wiki/Creating-a-systemd-service)

## Code repositories

- Vanilla: [Server](https://github.com/cmangos/mangos-classic) and [Database](https://github.com/cmangos/classic-db)
- TBC: [Server](https://github.com/cmangos/mangos-tbc) and [Database](https://github.com/cmangos/tbc-db)
- WotLK: [Server](https://github.com/cmangos/mangos-wotlk) and [Database](https://github.com/cmangos/wotlk-db)

### Automatic releases of server binaries for Windows

- [Vanilla](https://github.com/cmangos/mangos-classic/releases)
- [TBC](https://github.com/cmangos/mangos-tbc/releases)
- [WotLK](https://github.com/cmangos/mangos-wotlk/releases)

### Automatic releases of mangos DB as single SQL file (requires other DBs to be installed/updated manually)

- [Vanilla](https://github.com/cmangos/classic-db/releases)
- [TBC](https://github.com/cmangos/tbc-db/releases)
- [WotLK](https://github.com/cmangos/wotlk-db/releases)

## Bug Reports

Bug reports for all expansions can be made [on the issue tracker on this repository](https://github.com/cmangos/issues/issues). Note that there is a separate tracker on the wotlk-db repository, but this is mostly for historic reasons.

### Want to help us test and resolve issues?

- [Issues that need replication](https://github.com/cmangos/issues/issues?q=is%3Aissue+is%3Aopen+label%3A%22Info%3A+Needs+Replication%22)
- [Issues that need testing](https://github.com/cmangos/issues/issues?q=is%3Aissue+is%3Aopen+label%3A%22Info%3A+Needs+Testing%22)

## Misc

### CMaNGOS-related Tools

- [PHP library that can be used for account registration and authentication page](https://github.com/Laizerox/php-wowemu-auth)
- [Guide on how to use the above library](https://jimmyb.ninja/post/1582196188)
- [A simple user registration website based on the library](https://github.com/jimmybrancaccio/cmangos-starter-website)
- [Spell Viewer / Editor](https://github.com/sidsukana/QSpellWork/releases/latest)
- [GUI designer for EventAI scripts, DBscripts, and other random parts of the DB](https://github.com/killerwife/cmangos-designer/releases/latest)
- [Database editor for TC/AC/CMaNGOS](https://github.com/BAndysc/WoWDatabaseEditor)

### CMake-to-Boost known compatibility table

There have been reports of version mismatches between boost and cmake causing problems. If you encounter any such problems [check this list](https://github.com/cmangos/issues/wiki/CMake-to-Boost-Version-Compatibility-Table) and feel free to add the combination you were using.
