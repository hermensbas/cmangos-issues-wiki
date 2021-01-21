# What is the difference between the various platforms? Such as Mangos-zero, Trinity, Vmangos, and Cmangos

* TL;DR Nobody knows for sure. Other than their content focus, in example; Vmangos for vanilla, Trinity for WOTLK, Cmangos covers multiples and tries to apply fixes for one to the others so we are not unnecessarily duplicating work.

The short answer is **"probably not much"** but it is nearly impossible to tell for sure without someone combing through the code of each platform to compare.  All have the same general goal and at one point in time shared a code base. Over the years different design decisions have resulted in systems that function similarly but are probably implemented in different ways.  

### Yeah, but what does that mean for me?
Cmangos seems to have the most active public platform, which means we are frequently working on fixing bugs or features. The Devs are very responsive, if you give them the [Needed Information](https://github.com/cmangos/issues/wiki/On-Help-and-All-Things-Support) and have done at least some of your own homework. Like reading the FAQ, searching through Discord chat or the forums for your issue. Chances are the question has been answered before.

### But which is best?
As for content completeness, again it is impossible to say which is best. We'd like to think we have more stuff done as we seem to be more active than other platforms but there is no way to know and we are probably bias.


# What should I do when I encounter a problem?
* In general, read the log file and see if you can work out the problem from there on your own; if you can't, seek out help on:
  * Discord: https://discord.gg/Dgzerzb
  * IRC ([#cmangos](irc://irc.rizon.net/#cmangos))
  * the [cmangos.net forums](https://forum.cmangos.net/)
* Every application generates a log file somewhere that can be opened and reviewed.
  * For compile problems: Look into the log, on *nix you can create a log with `make > compile.log 2>&1`
  * For problems with the server: Look for the file, *Server.log*, in your server's home directory.

### I'm a beginner and want to understand how CMaNGOS works, where should I get started?
* See the [Beginner's Guide](https://github.com/cmangos/issues/wiki/Beginners-Guide-Home).

### How do I install CMaNGOS?
* See the [Installation Instructions](https://github.com/cmangos/issues/wiki/Installation-Instructions).

### How do I create a systemd service for CMaNGOS?
* See the [Systemd service guide](https://github.com/cmangos/issues/wiki/Creating-a-systemd-service).

### Error: "MySQL is not recognized as an internal or external command"
* You need to add MySQL to your path environment so that windows recognizes the command by default. See [here](http://dev.mysql.com/doc/mysql-windows-excerpt/5.1/en/mysql-installation-windows-path.html) for a walk through from MySQL.

### I have issues with BOOST during compilation / CMake generation steps and i'm on Windows!
* Check BOOST_ROOT and BOOST_LIBRARYDIR environmental variables, check [this](https://github.com/cmangos/issues/wiki/CMake-to-Boost-Version-Compatibility-Table) page for version compatibility (often all it takes to fix is to roll back the boost version or upgrading CMake).

### My server has errors when I try to start it
* First you should review the [Installation Instructions](https://github.com/cmangos/issues/wiki/Installation-Instructions) again to be sure you didn't miss any steps and that every step was done according to the instructions.  
* Second, search the forums or Discord for a solution (most errors have been encountered before and so there is usually a thread someone on the forums discussing it).
* Third, if you can't find any answers, use one of the methods mentioned [above](#what-should-i-do-when-i-encounter-a-problem) to ask the developers for help.

### Error in mangosd application:
```
ERROR:  [A] You have: --> _version_  
ERROR:  
ERROR:  [B] You need: --> _version_
```
* You need to update your database to the correct version to match the core.
* See the [here](https://github.com/cmangos/issues/wiki/Installation-Instructions#basic-concept-of-database-filling) in the Installation Instructions for details.

### I cannot login to my server
If your server is running and you just can't connect to it then there are several possible issues:
* Ensure that the realmd application is running; if not, start it up and check for errors if it doesn't stay open.  
* Ensure that the mangosd application is running; if not, start it up and check for errors if it doesn't stay open.
* Make sure that the following fields from the `realmlist` table (realmd database) match up to their corresponding values in your _mangosd.conf_ configuration file:  

  | realmlist | mangosd.conf    |
  |:---------:|:---------------:|
  | id        | RealmID         |
  | port      | WorldServerPort |

* Make sure that your _realmlist.wtf_ file in your game client folder is set to the address of your server. The content of the file should only have three phrases:  
    >set realmlist _address_  

  * If the server is on the same computer as the client then you can just use "127.0.0.1" as the address:  
  >set realmlist 127.0.0.1  

  * Otherwise the address should be the same as the "address" field from the `realmlist` table (realmd database).  

* If your server is hosted on a remote machine and/or you're using an IP address other than 127.0.0.1, then you probably have to update your realm address field in the database
  * Open the mysql client on your machine (mysql -p)
  * Run the following command (don't forget to replace the placeholder text with your values): ```UPDATE realmlist SET address='your.ip.address.here' WHERE id='id_of_the_realm_you_want_to_edit';```
  * You can get a list of all your realms with the following: ```SELECT * FROM realmlist;```

* Ensure that the user account you are trying to log in with is created:
  * See the [Installation Instructions](https://github.com/cmangos/issues/wiki/Installation-Instructions).
  * To add an account, type the below line directly into the server command prompt (mangosd) replacing $accountName with the name of the account and $accountPassword with the password to be used:  
  `account create $accountName $accountPassword`

* Don't use an email address as a username.  

* Delete or rename wow.mfil and wow.tfil files.  

* ONLY use wow.exe to start up the client, NEVER use launcher.exe (client versions 4.x and up require wow.exe to be patched prior as well).

### My client still connects to a different host/address
* Add in your _/WTF/config.wtf_ file: (SET realmlist "127.0.0.1") before (SET accountName "youraccount")

### MaNGOSd or/and Realmd instantly closes when I start them
* Run mangos in command line, terminal, or git bash instead; then you will see the on-screen error output and be able to continue from there.
* Make sure there are no other processes using the required ports (default 8085 & 3724).
* Also check realmlist table column timezone, this kind of "instantly closes" could write a 0 in this field and realm never will be accesible, change to 2 (EEUU MaNGOS default setup) or 1 (development) or 5 (tournament) or 26(PRT) try the various options until 59, but avoid a timezone 0 because u cant log on to a realm disable. 

### I play TBC or WotLK and cannot access the Blood Elves, Draenei, Worgen or Goblins
* You need to set the expansion of your account to 1/2/3 (for TBC/WotLK/Cata). See [[Installation Instructions]].

### I play WotLK/Cata and cannot access the Death Knight
* You need to set the expansion of your account to 2 or 3 (2 for TBC, 3 for Cata)
* You need to level a character to level 55 OR
* Change the config option "MinLevelForHeroicCharacterCreating" in your mangosd.conf OR
* Set your account to be a GM Account (see next question)

### How can I use GM commands?
* You need to set your GM-Level. See [[Installation Instructions]].

### Npcs directly evade when I try to attack
### All Npcs are friendly or neutral
### All Gameobjects around me sparkle
* You need to turn GM mode off: `.gm off`
* Maybe you still have invisibility on, try `.gm visi on`  

### How do I make custom items?
* CMaNGOS developers do not actively support custom items as we are focused on true emulation. That being said, you can always ask for help on the forums or lookup some guides around the internet. If you are up to the task, check out the [item_template](https://github.com/cmangos/issues/wiki/Item_template) wiki entry to get started from the ground up.

### The ".gm fly" command doesn't work
* This command does not work for classic core. If you are on another core, check your syntax and make sure you installed everything correctly.  

## How do I update?

### Updating the source code
* Open a Git Bash (see [[Installation Instructions]]) in your C:\Mangos or ~/mangos (your base directory)
* `cd mangos` (This assumes you followed the Installation Instructions, and the directory where your sources are located in C:\Mangos\mangos or ~/Mangos/mangos
* Invoke `git pull` to update
* `cd src/bindings/ScriptDev2` (This step and the next only if you also want to update SD2 and you had it installed)
* Invoke `git pull`

### Compiling and installing the update
* You need to compile core and SD2 just like you did before in your first setup (See [[Installation Instructions]] ).

### Fetching new content from the database provider
* This depends on your database provider, you might want to update your SVN or Git clone of the database.

### Updating the database
* Even if your Database provider did not ship new updates, you still might have to update your database content due to core changes.
* In this case the easiest process is to rerun the installer script from your DB-provider.
* If you don't want to reset the database to a clean state (for example because you added some custom things), then you _might_ need to update manually.
* To check if you need a manual update, just start the mangosd and check if a database error on start is printed.
* If it is, read the error message carefully (you can read it more easily from the file Server.log).
