What follows is an explanation of all the pieces to CMaNGOS from a beginner's perspective so that you can better grasp _why_ everything works. Even if you follow the instructions step-by-step, you may end up with a working server but have absolutely no idea how or why which makes it difficult to replicate, make changes, or fix things.

# Github
As described earlier, Github is a networking tool and a location to store data. In most cases, the data is code for various applications. Users can follow certain projects and comment on things while also contributing by suggesting changes, giving feedback and collaborating with others.

### CMaNGOS Repositories
The CMaNGOS project has a repository located at [https://github.com/cmangos](https://github.com/cmangos) which itself contains sub-repositories for each version of WoW currently supported. Each repository contains an assortment of folders and files which make up the code structure of all "server side" applications needed to host a WoW server.

When you follow the installation instructions you will be directed to retrieve the code from these repositories and store them on your local computer. You will then use a compiler to compile the code which produces a bunch of files and applications. 

### Commits
When things are changed on a repository it is referred to as a "commit" and assigned a unique tag to identify it. Commits can only be completed by users with the proper permissions to a repository to keep the process stable. This way any user can submit a suggested change but only the developers with the most experience can actually update the repository.

### Issues/Bugs
Bugs are typically reported and tracked on Github via the "Issues Tracker." CMaNGOS uses a centralized issue tracker for all repositories located [here](https://github.com/cmangos/issues/issues) instead of having multiple trackers for each individual version. Until you really know what you are doing, it is recommended that you don't start off submitting what you think are bugs into the issues tracker. Most of the time (for newbies), it is something you missed with the installation or configuration steps. Once you get a handle on everything, then you can start submitting bugs when you come across them (and you definitely should, it is the only way the developers will know if something needs fixing!).

# cmangos.net Forums
The forums at [cmangos.net](http://cmangos.net/) are where you go to ask questions and get help as well as make suggestions or provide feedback. Check it out and register an account! Everyone is very friendly and helpful and can answer just about any question or issue you have. That being said, please try to search for your issues in the installation instructions and forums before posting as there may already be an answer somewhere.

# MySQL Server and Databases
At the beginning of the installation instructions you are advised to setup a MySQL Server and have it running before continuing. There is no guide for setting up a MySQL Server within the CMaNGOS project because MySQL does not exist solely for CMaNGOS, in fact it is used by a _lot_ of different applications around the world. Subsequently you will find that there are numerous guides for setting up and configuring MySQL servers and other products from MySQL all over the internet. Do some google searches and you should find one that suits your needs.

The MySQL Server houses a vast amount of information broken down into databases. These databases tell the CMaNGOS game what actually exists in each server including: account names and passwords, characters, inventories, objects, items, npcs, enemies, loot, bosses, quests, guilds, resource nodes, etc. Basically, if you have an "empty" database and you log in to your game server, nothing will exist. I would just be a big empty world. You could think of the game server as a castle but it only has the terrain, a moat, walls and nothing else. When you link the game server to a database, it then populates the castle with a gate, drawbridge, windows, guards, weapons, food, and any other objects that the player can interact with or see.

Within each database you will find a number of "tables" which can be thought of like different excel spreadsheets which have the actual information. So in descending order, here is a breakdown of a MySQL Server:

**MySQL Server > Database > Table > Information**

![](http://i.imgur.com/3VdQ0yn.jpg)

It is highly recommended that you obtain an SQL Client (such as SQLyog) as it will really help you to visualize what is going on in the database and how it is structured.

## Where is this server?
The MySQL Server application will run in the background of your computer (for windows users you can see it in the "Services" tab of Task Manager):

![](http://i.imgur.com/VtZjLAk.png)

You can start up and shutdown your MySQL Server at will but it will need to be running in order for your game server to access the database. You may find it beneficial to pick up an SQL server utility which monitors your SQL server and gives you a simple menu to start and stop it from.

## CMaNGOS Databases
Once you have a MySQL Server running and finish the installation instructions for CMaNGOS you will find four new "databases" inside: realmd, characters, mangos, and scriptdev2. What follows is a quick summary of what each database contains.

### realmd database
This database contains the game server and player account information. Within the database you will find a table called realmlist which contains the information for directing your WoW game client to your game server. There are also tables containing the accounts for logging into your game server as well as banned accounts and a few other tables for similar information.

### characters database
This database contains multiple tables which store the information relative to each character in the game: what their skills are, what talents they've selected, the guild they belong to, what is in their inventory, etc.

### mangos database
This database contains everything about the actual game world: items, resource nodes, npcs, enemies, quests; everything down to the last crate stacked up in a corner of Stormwind. This database is obviously the largest.

### scriptdev2 database
This database is for special "scripts" which direct events that occur in the game. A script is exactly what it sounds like: a set of directions. Only these directions are for non-player creatures and objects to follow (think of it like the script to a play but the play is based on what the audience is doing). How do Stormwind guards know to patrol paths around the city and attack bad guys when they show up? A script tells them. Some scripts are built into the game itself while others are mapped out in the mangos database. ScriptDev2 is a more advanced system used for complicated scripts like boss fights and big events.

# Executable Applications
Executable applications (often referred to as "binaries") are part of the files created when you finish compiling the code. These particular files end with .exe as you may have noticed many applications on a computer do. There are really only two important executable files generated from the CMaNGOS code: realmd.exe and mangosd.exe. When you "start up" a server you will really just run both of these applications and let them do all of the work. If there are issues with your configuration or databases, they will give you detailed error messages advising what needs to be looked at. Your server will continue to operate as long as these two applications are running.

### realmd
The realmd.exe file is the first level of connectivity with your WoW client. When the game starts it will try to connect to a realmd type server. When you type in your login information realmd attempts to match it with the accounts it has stored in the database and then moves you on to select a realm.

### mangosd
The mangosd.exe file is the actual game server itself (known more commonly as a realm). While it is running you will see all sorts of messages appearing while events are going on and you can even type commands into it for the server to execute.


# Configuration Files
Part of the installation instructions will have you moving several text documents over to your "run" folder and renaming them so that they end with .conf. These are the configuration files that determine how your server will operate. All you have to do is edit the values according to the instructions provided inside each one to make things run how you want them to.

### realmd.conf
This file is used to tell your realmd.exe application which database to use to store account information. You can also configure some basic features for locking accounts and banning IPs that attempt to login with bad credentials too often.

### mangosd.conf
Perhaps the most important configuration file, mangosd.conf contains a multitude of variables which (most importantly) tell your mangosd.exe application which databases to use for characters, accounts, and the game world. You can also adjust a number of different settings for how the realm behaves such as xp rates, pvp, and much more (just look through the document and read the instructions to see what all you can change).

### scriptdev2.conf
There is only one thing to configure on this file and that is to tell your mangosd.exe application which scriptdev2 database to use.

### ahbot.conf
This is an optional configuration file which, if added to your "run" folder will enable you to use the AH bot (a bot system that simulates an active auction house that buys and sells things to make it feel like there are more players on the server).

### mods.conf
Another optional file which will allow you to enable or disable special modifications for your server that are not part of the standard game.

# Game Resources
One of the last steps in the installation instructions has you extract "resources" from your WoW client. This process produces four folders that then need to be moved into your "run" folder in order for the game server to function: dbc, maps, vmaps, and mmaps.

### DBCs
DBCs are game files which provide details on things like spells. You might notice that the majority of "simple" spells and items are contained within the databases whereas more complex ones can only be stored in the DBCs.

### MAPS
Pretty straight forward: the maps folder contains all of the physical maps that the server will be running (the actual world environment).

### VMAPS
Vmaps are like overlays for maps that specify how "line of sight" (LOS) is calculated for players and creatures. So basically they tell the game server where objects are that obstruct LOS like trees, buildings, and crates.

### MMAPS
Mmaps are similar overlays that tell the server where to route creatures and NPCs so that they don't run over top of rocks and fence posts. They aren't technically necessary but they greatly enhance the game experience and there isn't really a good reason _not_ to use them. Note that creating the mmaps can take several hours so you may want to start the process before going to bed or leaving for work. When you extract resources from the client using the ExtractResources.sh script it will tell you this and even give you an option to delay the mmaps.

## Okay that's great, now what?
Now we move on to how all of these things work together.

Next: [How Everything Fits Together](https://github.com/cmangos/issues/wiki/Beginners-Guide-How-Everything-Fits-Together)

[Beginner's Guide Home](https://github.com/cmangos/issues/wiki/Beginners-Guide-Home)