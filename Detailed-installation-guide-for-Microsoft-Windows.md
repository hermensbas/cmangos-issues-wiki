# Welcome

Welcome to the **C**ontinued **Ma**ssive **N**etwork **G**ame **O**bject **S**erver! :tada:

This step-by-step guide is intended to help people to install a CMaNGOS World of Warcraft server on their Windows computer. If you need installation instructions for macOS or Linux, see the [More Information](#more-information) section. Information about updating an already installed server is provided in the [Updating](#updating) section of this file.

# Table Of Contents

[Welcome](#welcome)

[Table Of Contents](#table-of-contents)

[What Should I Know Before I Get Started?](#what-should-i-know-before-i-get-started)
* [Versions](#versions)
* [Releases](#releases)
* [More Information](#more-information)
* [32 or 64 Bit?](#32-or-64-bit)

[Toolchain](#toolchain)
 * [Boost](#boost)
 * [CMake](#cmake)
 * [Git](#git)
 * [MySQL](#mysql)
 * [Notepad++](#notepad) (Optional)
 * [Visual Studio](#visual-studio)
 
[Cloning the repositories](#cloning-the-repositories)
* [Location](#location)
* [Core](#core)
* [Database](#database)

[Compilation](#compilation)
* [Configure CMake](#configure-cmake)
* [Compile with VS2017](#compile-with-vs2017)

[Database Setup](#database-setup)
* [Creation](#creation)
* [Initialisation](#initialisation)
* [Filling](#filling)

[Map Extraction](#map-extraction)

[Finishing touches](#finishing-touches)
* [Configuration](#configuration)
* [Running](#running)
* [Account Creation](#account-creation)
* [Ingame commands](#ingame-commands)
* [Shutdown](#shutdown)

[Updating](#updating)
* [Released binaries](#released-binaries)
* [Self compiled binaries](#self-compiled-binaries)
* [Database Update](#database-update)

# What Should I Know Before I Get Started?

### Versions

There are three versions of CMaNGOS: **Classic**, **The Burning Crusade**, and **Wrath of the Lich King**. The fourth version, **Cataclysm** is currently not maintained. Each version consists of one core git repository and one database git repository (found under https://github.com/cmangos):

| Repo\Version | Classic        | TBC        | WotLK        |
| ------------ | -------------- | -----------| ------------ |
| **Core**     | mangos-classic | mangos-tbc | mangos-wotlk |
| **DB**       | classic-db     | tbc-db     | wotlk-db     |

**Note:** When following this guide, you will sometimes have to pick the command/path appropriate to the version you would like to install. You will have to replace the `VERSION` part of them with `classic`, `tbc` or `wotlk`, i.e. if you are asked to get to `C:\mangos\mangos-VERSION` and you are installing WotLK, you have to go to `C:\mangos\mangos-wotlk`. The screenshots will show the paths for the Classic version.

### Releases

The compilation of the server core and extractor tool binaries is optional. If you do not plan on changing the code yourself, you can download the precompiled binaries from the release pages of the core repositories on Github. Here are the links to the download pages:

* [https://github.com/cmangos/mangos-classic/releases](https://linkify.me/Dt19dgh)
* https://github.com/cmangos/mangos-tbc/releases
* https://github.com/cmangos/mangos-wotlk/releases

We will provide more information about how to set up a server with released files when it will be possible.

### More Information

This guide is intended only for Windows and provides one of many ways to set up a CMaNGOS server. You can find a [more detailed installation guide](https://github.com/cmangos/issues/wiki/Installation-Instructions) (including alternative programs, Linux/Mac setup, etc.) in the [Wiki](https://github.com/cmangos/issues/wiki). If you get stuck you can find us here:
- http://cmangos.net (forum)
- Discord: https://discord.gg/nSaXpCn
- **#cmangos** channel on **irc.rizon.net**
- you can create an new issue in our [Github bug tracker](https://github.com/cmangos/issues/issues)

### 32 or 64 Bit?

This section will most likely not be of any concern to most people, as it is highly unlikely they have 32-bit hardware/OS. If your system is very old and you want to make sure you run a 64-bit version of Windows, press **WinKey+Pause** (or navigate to the **System** settings in the Control Panel). You should see a row named **System type** in the list there, which should read **64-bit Operating System**. If that is the case, you can ignore the rest of this section and follow the guide to the letter.

![architecture](https://user-images.githubusercontent.com/8838573/27604263-1cd25e72-5b79-11e7-9561-de8e6a0499a1.PNG)

32-bit/64-bit refers to the instruction set architecture (ISA) of your computer's central processing unit (CPU). Generally speaking, 64-bit processors can run instructions sets (parts of a program) that are twice as big and the program, therefore, runs faster. They are however able to run 32-bit programs as well, while 32-bit processors are unable to run 64-bit programs. The same goes for operating systems. If you have a 64-bit processor but a 32-bit Windows version, you will not be able to run 64-bit programs.

In the context of this guide, that means if you have either a 32-bit processor or Windows version, you will have to adjust the instructions given here to that fact. You will have to download/install 32-bit programs and set it as target architecture during compilation. You can usually recognize the correct link/file by a part of its name that will read something like **32**, **32bit**, **x86**, etc. If you run into problems while compiling or running a 32-bit version of CMaNGOS, you can find information about how to contact the team in the [above section](#more-information).

**Note:** While **x86** refers to the 32-bit architecture, **x86_64** or **x86-64** refers to the 64-bit architecture (read "I can only process 32-bit" vs. "I can process both 32-bit and 64-bit").

# Toolchain

These are programs you will need to set up the database and compile the core. This section will explain where to download and how to install them. **If not otherwise noted in the programs installation instructions, the default settings apply.** After downloading them all into a separate folder, it should look something like this:

![installers](https://user-images.githubusercontent.com/8838573/27418828-e5ebb048-571d-11e7-900f-bda30e015fe4.PNG)

## Boost

- Go to: [http://sourceforge.net/projects/boost/files/boost-binaries/](https://linkify.me/AxSRpv8)
- Select a version number not ending in `_bX` (those are beta versions), e.g. click `1.69.0`. (Confirmed working as of 2019-01-09.)
- Download the executable file containing `msvc-14.1-64`, e.g. `boost_1_69_0-msvc-14.1-64.exe`. (MSVC-14.1 is the Visual Studio 2017 C++ compiler, 64 stands for the 64-bit architecture. If using Visual Studio 2019, try MSVC-14.2 rather than MSVC-14.1)
- Execute the downloaded file. During the installation you will be asked to set the installation path, if you change it, remember it. It is needed in the next step.
- Add the `BOOST_ROOT` environment variable (**Note:** You might have to relog/restart afterward, so every program can see this variable):
  - Press **WinKey+Pause** (or navigate to the **System** settings in the Control Panel).
  - Click on **Advanced system settings**.
  - Click on **Environment Variables**.
  - Click on the bottom **New** button (Note: there are two, we need the one under **System variables**).
  - As **Variable name** enter `BOOST_ROOT`, as **Variable value** enter the path you installed boost to
    (`C:\local\boost_X_XX_X` by default, depending on which version you downloaded).

  ![boost_root](https://user-images.githubusercontent.com/8838573/27419813-198fba5c-5723-11e7-8908-883eb827e415.png)
  

## CMake

- Go to: [https://cmake.org/download/#latest](https://linkify.me/8NcB9r6)
- Download the **Windows win64-x64 Installer** (currently `cmake-3.8.2-win64-x64.msi`) and install it.

## Git

- Go to: [https://git-scm.com/download/win](https://linkify.me/uRS1bFS)
- Confirm the download if it is the architecture you want (32 or 64 bit). Otherwise, abort and select the correct version.
- During installation make sure the following options are checked:
  - Git Bash Here:
  
  ![git1](https://user-images.githubusercontent.com/8838573/27420240-3f87c61c-5725-11e7-9458-5bab126aa6b0.PNG)

  - Use Git from the Windows Command Prompt:
  
  ![git2](https://user-images.githubusercontent.com/8838573/36945424-2f6b30d2-1fae-11e8-9989-a77740cf7d44.PNG)

  - Use MinTTY:
  
  ![git5](https://user-images.githubusercontent.com/8838573/27420244-448c01aa-5725-11e7-9827-1b4efaf3c9b9.PNG)

## MySQL

- Go to: https://dev.mysql.com/downloads/installer/
- Download the web installer. If you have no internet during setup you can download the full 400 MB installer instead.

  ![mysql1 1](https://user-images.githubusercontent.com/8838573/27420380-fef2b930-5725-11e7-8db9-0db57591ed49.PNG)

- Start the installer and select Setup Type **Custom**:

  ![mysql3](https://user-images.githubusercontent.com/8838573/27420541-a0090e78-5726-11e7-92e3-053d58e29517.PNG)

- Add **MySQL Server** and **MySQL Workbench**:

  ![mysql4](https://user-images.githubusercontent.com/8838573/27420571-c8ba87ca-5726-11e7-93ee-351109b9ede3.PNG)

- If there are missing requirements reported on the next page, select them and click **Execute** if possible:

  ![mysql5_req](https://user-images.githubusercontent.com/8838573/27420697-66dcb1f8-5727-11e7-9bc9-b534c5054a1e.PNG)

- You will have to define the **MySQL Root Password**. This will be the admin password to your MySQL server so make sure to remember it! The root user will have access to all databases. We will create another user later in the process which will only have access to CMaNGOS databases.

  ![mysql7](https://user-images.githubusercontent.com/8838573/27420887-3554e1ae-5728-11e7-9037-bb64b886ef4d.PNG)

- After the installation has finished, start the **MySQL Workbench** program and click on the **Local instance** button. In the popup that opens, set the checkbox, and enter your root password.

  ![mysqlx](https://user-images.githubusercontent.com/8838573/27421017-c6639bcc-5728-11e7-9741-54086ce87963.PNG)

- Add the MySQL servers path to the `Path` environment variable:  (**Note:** You might have to relog/restart afterward, so every program can see the updates to the variable)
  - Press **WinKey+Pause** (or navigate to the **System** settings in the Control Panel).
  - Click on **Advanced system setting**.
  - Click on **Environment Variables**.
  - In the bottom part of the new window (under **System variables**) look for the variable called **Path**, select it, and click on **Edit**.
  -  **Note: This field is a list of values, separated by `;`. Do not delete the entries that were already there, or some programs might stop working!**
  - Select the **Variable value** field and make sure the cursor is at the end of the field and no text is selected (press **EndKey** or **ArrowRightKey**).
  - Add the path where your MySQL server was installed, prefixed by a semi-colon (by default `;C:\Program Files\MySQL\MySQL Server 5.7\bin`) and save the changes by clicking **OK**.

  ![mysql_path](https://user-images.githubusercontent.com/8838573/27421847-62bd1d24-572c-11e7-9260-bd2069af5ad4.PNG)

## Notepad++

 - **Notepad++ is completely optional.** It is an improved version of the text editor that comes with Windows. You will have to edit a few files during installation, which you can do with the standard editor, but it is recommended doing it with Notepad++, as it has some handy features:
   - Open files from the context (right-click) menu:
   
     ![npp_context](https://user-images.githubusercontent.com/8838573/27422058-252ea206-572d-11e7-8409-284dc2b1c3cd.PNG)
   
   - Recognizes Linux style line endings. (Windows apparently thinks it is a typewriter and uses two symbols, CR and LF - **c**arriage **r**eturn and **l**ine **f**eed - for new lines instead of just LF like Linux does. This is why some files mysteriously appear to be written in one line.)
   - Line numbers.
   - Open multiple files at once.
   - Remembers opened files and unsaved changes between sessions.
- Go to: https://notepad-plus-plus.org/download/
- Download (32bit recommended since it has more plugins available) and install it.
- Make sure **Context Menu Entry** option is enabled:

  ![npp](https://user-images.githubusercontent.com/8838573/27422282-d328dc28-572d-11e7-9d14-6043643daa6d.PNG)

## Visual Studio

- Go to: https://www.visualstudio.com/downloads/
- Under **Visual Studio Community 2017** click on **Free Download**.
- Open the installer. When asked to select Workloads, check **Desktop development with C++** and then click **Install**:

  ![vs1](https://user-images.githubusercontent.com/8838573/27422646-444323ea-572f-11e7-9c0c-d92930ccc4d8.png)

- Start **Visual Studio 2017**. You will be asked if you want to sign in, but it is not needed:

  ![vs2](https://user-images.githubusercontent.com/8838573/27422852-f8f5c3ec-572f-11e7-9430-c95d9c56b22b.PNG)

- In the next window, leave the Development Settings as they are (General), but feel free to select another theme:

  ![vs3](https://user-images.githubusercontent.com/8838573/27422919-2f51bc48-5730-11e7-9066-b5011e59ed82.PNG)

- Close Visual Studio for now.

# Cloning the repositories

A git repository is basically just a normal directory that contains some hidden files, that the git program (or some other program) can use to manage different versions of that directory. In this step, we will "clone" the repositories from Github, which means creating an exact copy of them on your hard drive.

### Location

You can basically follow this guide from any location on your hard drive. However, we will assume you have created an empty directory called **mangos** on your C drive: `C:\mangos`. If you want to work in another location, you will have to adjust some of the provided commands/locations. We also assume you have installed the [Git Bash Here](#git) and [Edit with Notepad++](#notepad) commands to the Windows context menu.

Navigate to `C:\mangos` in the Windows Explorer, **Right-Click** into the empty area and select **Git Bash Here**:

![git_bash1](https://user-images.githubusercontent.com/8838573/27423501-0edc2bae-5732-11e7-8763-f54e2b63427b.PNG)

A new window should open with two lines of text:

1. `user@device MINGW64 /c/mangos`
   - This line shows the active user and the working directory. You can ignore the MINGW64.
2. `$ ` 
   - This line is the command prompt. It waits for you to write a command and press **Enter**.

**FYI:** Git Bash uses Linux style paths, which means:
- Paths use `/` (forward slash) instead of `\` (backward slash).
- Your base directories are not the hard drive partitions, but the single "root directory" `/`, which contains all the hard drives (and some other stuff). So `/c/` points to your `C:\` and `/d/` points to `D:\`.
- There is a shortcut to the users "home" directory, which is `~`. The Windows path hidden behind that is `C:\Users\YourUserName`. So if Git Bash says you are in `~/Desktop` you are actually in `C:\Users\YourUserName\Desktop`.
- There are absolute paths (starting with `/` or `~`), and relative paths (not starting with `/` or `~`). Relative paths point to a location relative to the working directory. Every directory contains a directory `..` which points to its parent (the directory one step closer to the root directory), and a directory `.` which points to itself (executing binaries is prefixed with `./`).
- Use `cd /absolute/path/to/something` or `cd relative/path/to/something`to change your working directory. You can use `cd ..` to go one directory back, `cd ../..` to go two directories back, etc.
- When you are entering long path names, you can use the **Tab** key to auto-complete them. E.g. if you have already entered `cd /c/man` and then press **Tab**, the command prompt will autocomplete it to `cd /c/mangos` (as long as there are no other directories in `/c/` that start with `man`).
- For more information see https://en.wikipedia.org/wiki/Path_(computing)

### Core

**Note:** You need these files even if you use the precompiled binaries since some of the database creation scripts are contained in this repository. This command creates a copy of the Github repository on your hard drive.

- Copy the command (**Ctrl+C**):
```
git clone https://github.com/cmangos/mangos-classic.git
git clone https://github.com/cmangos/mangos-tbc.git
git clone https://github.com/cmangos/mangos-wotlk.git
```

- In the Git Bash window, **Right-Click** and select **Paste**, or press **Shift+Insert** (for historic reason the usual copy/paste keyboard shortcuts do not work in most command-line interfaces).

  ![git_bash2 1](https://user-images.githubusercontent.com/8838573/27424959-1d8d9bd8-5737-11e7-96e6-51e2fd082c5a.PNG)

- Press **Enter** to confirm the command.
- Wait for download to finish.

### Database

- Copy the command:
```
git clone https://github.com/cmangos/classic-db.git
git clone https://github.com/cmangos/tbc-db.git
git clone https://github.com/cmangos/wotlk-db.git
```
- Paste it in Git Bash and press **Enter** to confirm the command.
- Wait for download to finish.

  ![git_bash3](https://user-images.githubusercontent.com/8838573/27425094-8f2e828e-5737-11e7-9b5d-6152d8462069.PNG)

# Compilation

### Configure CMake

- Start CMake.
- Set source directory to `C:\mangos\mangos-VERSION` and build directory to `C:\mangos\mangos-VERSION\bin\BuildDir` (see screenshot). You will have to create the `bin` and `BuildDir` directories if they do not exist. The `bin` directory is listed in the repositories `.gitignore` file, which means you can change its content without git noticing it. If you choose another location inside the repository for building, you will break the update process (see [Updating](#updating)).
- Click **Configure**

  ![cmake1 1](https://user-images.githubusercontent.com/8838573/27503014-cdfc8ffa-5878-11e7-9c54-cb5aa7fb1714.PNG)

- In the pop-up window select the compiler version. If you followed this guide you have **Visual Studio 15 2017 Win64**

  ![cmake2](https://user-images.githubusercontent.com/8838573/27503270-fcf143da-587a-11e7-9f11-a6f8e5fe4e81.PNG)

- Make sure the **BUILD_EXTRACTORS** option is checked. Then click **Generate**. *FYI: You can also activate the `BUILD_PLAYERBOT` or the `BUILD_AHBOT` option. Playerbot allows you to add other characters in your account as AI-controlled bots that follow you around. AHBot automatically adds new items to the auction house for reasonable prices to simulate an economy.*

  ![cmake3 x](https://user-images.githubusercontent.com/8838573/27503421-24a974f0-587c-11e7-93bb-91fe2d98aaa5.PNG)

- Once the console at the bottom says `Generating done`, press **Open Project**, which should open Visual Studio.

  ![cmake3 y](https://user-images.githubusercontent.com/8838573/27503456-751a2808-587c-11e7-8e87-ad93a4aab59a.PNG)

### Compile with VS2017

1. Wait until the loading has finished (see bottom of the window).
2. Choose **Release** and **x64** at the dropdown menus on top.
3. Press **Ctrl+Shift+B**, or **Right-Click** the topmost solution and select **Build Solution**.
4. Wait until the output log shows the **Build succeeded** message.

  ![vsx](https://user-images.githubusercontent.com/8838573/27503885-593bd7f8-5881-11e7-996f-5b53d1abd297.png)

- Assuming everything went well the binary-, library-, and configuration-files should now be in `C:\mangos\mangos-VERSION\bin\x64_Release`.

# Database Setup

### Creation

- Open **MySQL Workbench** and under **MySQL Connections** click on **Local instance MySQL57** to establish a connection to the MySQL server.
- In the new tab that opens, click the **Open SQL script file** button:

  ![db_create1 1](https://user-images.githubusercontent.com/8838573/27504640-4b545c3e-588e-11e7-847c-4767db8b4e36.png)

- Navigate to `C:\mangos\mangos-VERSION\sql\create\` and open the `db_create_mysql.sql` file.

  ![db_create1](https://user-images.githubusercontent.com/8838573/27504694-65694296-588f-11e7-96f0-e3ba46924dc7.PNG)

- By running this script, a new user and three new databases will be created. Make sure you have no text selected in the editor, then click the left dash symbol. See the output at the bottom of the window to make sure there were no errors.
  - **Note:** The new user is created in case people use their MySQL server for other stuff, as well as for security reasons. If you want to expose your server to the internet, **it is highly recommended to change the password** of this user in line 7 of the script (the string behind `IDENTIFIED BY`). **When closing the file, do not save the changes, or you will break the [update](#updating) process.**
  - **FYI:** If you want to run different versions of CMaNGOS at the same time (Classic/TBC/WotLK), you will have to rename the `mangos` DB (lines 1 and 9), the `characters` DB (lines 3 and 11) and the `realmd` DB (lines 5 and 13). The user creation (line 7) will need to be deactivated when creating a second or third server. Note that the middle dash button in Workbench executes only that part of the code, which has been selected in the editor, which might be helpful here.
  - **FYI:** If you change neither password nor database names, and you do not wish to change the standard server configuration, you can skip the [Configuration](#configuration) step later on.

  ![mysql13](https://user-images.githubusercontent.com/8838573/27504383-d7c121d0-5888-11e7-964c-ecfb38957176.PNG)
 
- You should now see the new databases (referred to as **Schemas** in Workbench) on the left. If not, click the refresh button.

  ![mysql14](https://user-images.githubusercontent.com/8838573/27504433-7c2372be-5889-11e7-82c1-066decf94b79.PNG)

### Initialisation

- **Double-Click** the `characters` database in the Schemas overview so that its name is written in bold. This marks the database as active, which means that table-specific SQL commands will be run on this database. If the database name is not written in a bold text after double-clicking it, restart Workbench and **double-click** again.
- Click the **Open script file** button above the editor:

  ![mysql12 1](https://user-images.githubusercontent.com/8838573/27504191-c818d0f0-5885-11e7-9205-091aeb828ed7.png)

- **Double-Click** the `characters` database in the Schemas overview and execute the `characters.sql` file found in `C:\mangos\mangos-VERSION\sql\base\`. (See output at bottom of the window to know when it is finished.)
- **Double-Click** the `realmd` database in the Schemas overview and execute the `realmd.sql` file found in `C:\mangos\mangos-VERSION\sql\base\`.
- **Double-Click** the `logs` database in the Schemas overview and execute the `logs.sql` file found in `C:\mangos\mangos-VERSION\sql\base\`.
- You can now close Workbench.

### Filling

- Navigate to the `C:\mangos\VERSION-db` directory in the Windows Explorer, **Right-Click** into the empty area and select **Git Bash Here**.

  ![db_install](https://user-images.githubusercontent.com/8838573/27504730-11175d3a-5890-11e7-8a24-0595b3a152a5.png)

- Enter `./InstallFullDB.sh` and press **Enter**.

  ![db_install1](https://user-images.githubusercontent.com/8838573/27504742-387882b4-5890-11e7-88b0-2059fc203625.PNG)

- In the Windows Explorer, **Right-Click** the newly created file `InstallFullDB.config` and select **Edit with Notepad++**.

  ![db_install2](https://user-images.githubusercontent.com/8838573/27504761-c5bfa24c-5890-11e7-8ab5-5a867200da5b.png)

- Change the `CORE_PATH` variable to `../mangos-VERSION` and save the file. 
  - **FYI**: The double dots mean we are going back one step in the directory tree, so it is assumed that the core repository has been cloned to the parent directory of the database repository. If you diverged from the guide's steps, adjust the relative path accordingly, or use an absolute path (see [Location section](#location)).
  - **Note:** If you changed the MySQL user name and/or password during the [database creation](#creation) step, you will have to change the `USERNAME` and/or `PASSWORD` variable here as well.
  - **Note:** If you changed the database name `mangos` during the [database creation](#creation) step, you will have to change the `DATABASE`variable here as well.

  ![db_install3](https://user-images.githubusercontent.com/8838573/27504838-61f4f4b8-5892-11e7-80f4-6d44cd1fc48e.png)

- In Git Bash, enter the `./InstallFullDB.sh` again, by pressing **ArrowUp** and **Enter** (it will now do something different since the `config` file is present).

  ![db_install4](https://user-images.githubusercontent.com/8838573/27504858-c044d6dc-5892-11e7-8bed-14c54d9e684a.PNG)

- Once the script finished you should see a message like this:

  ![db_install5](https://user-images.githubusercontent.com/8838573/27504869-dcf6d168-5892-11e7-8138-e142b861147e.PNG)

# Map Extraction

- **FYI:** This step deals with extracting terrain information from the client. This is used by the AI to generate the correct movement. Four different data types are extracted. One of them, mmaps, is optional, because its **extraction takes a long time (depending on your CPU, 30 minutes to several hours)**. Mmaps are required for correct NPC movement though, so it is **not** advised to skip mmap extraction. This step is sometimes also needed when updating, but only if the extraction process has been changed (it is always needed when first installing). If the files need to be updated, the server will crash on startup and write information about this to the log file.
- Acquire a clean copy of the correct WoW client version (1.12.1/2.4.3/3.3.5). *Note: It is recommended to do this step in a copy of the client directory, not the actual one you use for gaming since some temporary files are created. If you use a copy you can just delete it after you are done.* Your directory should look something like this (example from classic):

  ![extract1](https://user-images.githubusercontent.com/8838573/27504988-43cacbae-5895-11e7-851a-20938df59583.PNG)

- Go to `C:\mangos\mangos-VERSION\bin\x64_Release\Extractors` (or the `Extractors` directory inside the directory you extracted the precompiled binaries to) and copy all the files to the client directory:

  ![extract2](https://user-images.githubusercontent.com/8838573/27505052-81d047fc-5896-11e7-8c2e-e11ca14f6839.PNG)

- **Right-Click** into the empty area and select **Git Bash Here**. Enter the command `./ExtractResources.sh` and press **Enter**.
- The script will ask for settings, the recommended inputs are: 
  - y
  - Number of your CPUs cores/threads. If you are unsure how many cores/threads your CPU has, **Right-Click** the Windows Taskbar, select **Start Task Manager** and switch to the **Performance** tab:
    - On Windows 7 the number of graph windows you see under **CPU Usage History** corresponds with the number of cores/threads your CPU has. Example picture with 4 cores/threads:
    
        ![cores4](https://user-images.githubusercontent.com/8838573/27505757-0f2c74e8-58a8-11e7-8c81-a243dff798f1.png)
        
    - On Windows 10,  look for the line saying **Logical Processors**:
    
        ![cores8](https://user-images.githubusercontent.com/8838573/36945527-d655ed5a-1faf-11e8-865d-652c912ce73c.png)
        
  - nothing (leave line blank and press **Enter**)

  ![extract3](https://user-images.githubusercontent.com/8838573/27505090-98987422-5897-11e7-939d-9bc9f9bcdbee.PNG)

- You will be prompted to confirm your settings. Press **Enter** to do so and go do something else. **Like mentioned before, extraction takes a long time (depending on your CPU, 30 minutes to several hours). Wait until you see the command prompt again (`$ `).**

  ![extract4](https://user-images.githubusercontent.com/8838573/27505793-e9992ae0-58a8-11e7-8140-472ec56625e7.png)

- After the extraction is finished, copy the `dbc`, `maps`, `mmaps` and `vmaps` directories to `C:\mangos\mangos-VERSION\bin\x64_Release` (or the directory you extracted the precompiled binaries to).

  ![extract5](https://user-images.githubusercontent.com/8838573/27505326-58fea9e8-589d-11e7-9ce4-c71fd5ec8a63.PNG)

# Finishing touches

### Configuration

#### Note: If you have not changed the user password and database names during the [database creation](#creation) step above, and you do not plan on changing the standard configuration, then you can skip to [running](#running).

- **FYI:** You will have to start two binaries (`.exe` files) to launch the server, the `mangosd.exe` and the `realmd.exe` (*the **d** stands for **daemon** (**d**isk **a**nd **e**xecution **mon**itor). Both of the binaries read settings from a file that is passed to them by the `-c <config-file>` argument when starting them (see [below](#running)).
- The standard names for the configuration files are `mangosd.conf.dist` and `realmd.conf.dist`. They are copied to `C:\mangos\mangos-VERSION\bin\x64_Release` when compiling (or contained in the zip file of the precompiled binaries). **If you change the configuration, it is advised you rename the files to `mangosd.conf` and `realmd.conf`, so they will not be overwritten when [updating](#updating).** To do so, select the file and press **F2** or **Right-Click** it and select **Rename** from the context menu. Then remove the `.dist` at the end, and press **Enter**. If you do not see the `.dist` ending when trying to rename, see the note below.

  ![folder1 3](https://user-images.githubusercontent.com/8838573/27506163-f5d975ee-58b2-11e7-867e-3a94e08c809f.png)

- **Note:** By default, Windows hides the part of the file name behind the last dot (`.`) in it (the file type extension). If you try to rename the files and do not see the `.dist` ending:
  - Click on **Organize** in the top left and select **Folder and search options**.

    ![folder2](https://user-images.githubusercontent.com/8838573/27505964-f74c4dd4-58ad-11e7-9cec-9caff4ec99b5.png)

  - Uncheck the **Hide extensions for known file types** option and click **OK** or **Apply**.

    ![folder3](https://user-images.githubusercontent.com/8838573/27505979-66cc1b94-58ae-11e7-8146-cb39693f1db6.png)

  - Try renaming again.

- After changing the file names, **Right-Click** the `mangosd.conf` and select **Edit with Notepad++**. Change the values of `LoginDatabaseInfo`, `WorldDatabaseInfo`, and `CharacterDatabaseInfo` variables according to the changes you made (if you made any) during the [database creation](#creation) step and save the file with **Ctrl+S**.

  ![mangosd](https://user-images.githubusercontent.com/8838573/27506326-0b3f46ae-58b6-11e7-84a7-171d6c71b75a.png)
  
- **Right-Click** the `realmd.conf` and select **Edit with Notepad++**. Change the values of `LoginDatabaseInfo` variable according to the changes you made (if you made any) during the [database creation](#creation) step and save the file with **Ctrl+S**.

  ![realmd](https://user-images.githubusercontent.com/8838573/27506893-9e0f70aa-58c3-11e7-9205-60110984124f.png)

### Running

- In the Windows Explorer, navigate to `C:\mangos\mangos-VERSION\bin\x64_Release` (or the directory you extracted the precompiled binaries to). You have two options of doing the startup:

1. **Manual:** Run from Git Bash
    -  **Right-Click** into the empty area and select **Git Bash Here**.
    - Enter `./realmd.exe -c realmd.conf` (or `realmd.conf.dist` if you skipped the [Configuration](#configuration) step) and press **Enter**.
    - **Right-Click** into the empty area and select **Git Bash Here** again.
    - Enter `./mangosd.exe -c mangosd.conf` (or `mangosd.conf.dist` if you skipped the [Configuration](#configuration) step) and press **Enter**.
2. **Automatic:** Create shortcuts containing the arguments
    - **Right-Click** the `mangosd.exe`, chose either **Send to->Desktop (create shortcut)** or **Create shortcut** to create it in the same directory as the binaries.
  
      ![shortcuts1](https://user-images.githubusercontent.com/8838573/27507105-a6794b26-58c8-11e7-9650-1125e15af9fd.png)
  
    - **Right-Click** the newly created shortcut and select **Properties**.
  
      ![shortcuts2](https://user-images.githubusercontent.com/8838573/27507112-d0b96dd0-58c8-11e7-89ad-68e8b42e2b5c.png)
  
    - At the end of the **Target** field, add ` -c mangosd.conf` (or ` -c mangosd.conf.dist` if you skipped the [Configuration](#configuration) step).
  
      ![shortcuts3](https://user-images.githubusercontent.com/8838573/27507121-123c05ec-58c9-11e7-91c6-b1a072cce79a.png)
  
    - Repeat this for the `realmd.exe`, but add ` -c realmd.conf` (or ` -c realmd.conf.dist` if you skipped the [Configuration](#configuration) step) at the end of the **Target** field instead.

- Start the the `realmd.exe` first, then the `mangosd.exe`. The latter will take some time to start, watch for the `CMANGOS: World initialized` line. (Depending on your configuration, it will be visible only for a split second. See [next](#account-creation) step on how to change that.)
  
  ![start_server](https://user-images.githubusercontent.com/8838573/27507216-b69ba52e-58ca-11e7-88b7-87912ace65cd.png)

- When first starting the server, the Windows Firewall might ask for permissions. If you want players to connect over the local network or the internet, enable both checkboxes and click **Allow access** (for both `realmd` and `mangosd` binaries).
  
  ![start1](https://user-images.githubusercontent.com/8838573/27507252-98908788-58cb-11e7-8609-0b7357655255.PNG)

### Account Creation

- The `mangosd.exe` window will wait for commands. You can ignore the text scrolling through the window, it does not influence text input or deletion.
- **FYI:** If the scrolling text is bothering you, open the `mangosd.conf` file and change the value of the `LogLevel` variable to 0 (Mind the notes in the [Configuration](#configuration) section about the config being overwritten during updates).
  
  ![log](https://user-images.githubusercontent.com/8838573/27507342-5b1c9c00-58cd-11e7-8040-c13a1a76fac7.PNG)
  
- Creating a new account: `account create MyNewAccount MyPassword`
- Setting the expansion the account is allowed to access: `account set addon MyNewAccount 2`
  - 0: Classic (default value, this command is not needed when installing classic)
  - 1: TBC
  - 2: WotLK
  - 3: Cata
- Setting the access level to in-game commands: `account set gmlevel MyNewAccount 3`
  - 0: Player (default value)
  - 1: Moderator
  - 2: Game Master
  - 3: Administrator
- After successfully entering these commands you are ready to start the client and log in to the server. Make sure the `realmlist.wtf` file in the client directory only contains `set realmlist 127.0.0.1` before starting. If you want to save addresses of other servers, you can prefix their lines with `//`, like:

    ```
    set realmlist 127.0.0.1
    //set realmlist someRealmd.somewhere
    ```
### Ingame commands

- There are many useful in-game commands. When in-game, open the chat prompt by pressing **Enter**, write `.help` and confirm by pressing **Enter** again. This will show a list of commands available to your account in the chat window. Many commands show further in-game documentation when called without arguments (e.g. `.modify`).
- CMaNGOS has no dedicated documentation of these commands, if you want a list look through the source files, the database, or search the web for something like "mangos gm commands" (most commands are the same across open source servers).

### Shutdown

- In the `mangosd.exe` window, write `server shutdown 1` (the number represents delay in seconds) and press **Enter**.
- In the `realmd.exe` window, press **Ctrl+C**.

# Updating

- **Note:** The `git pull` command used below might not work if you changed files inside the repositories (except for the `bin` directory inside the core repository and the `InstallFullDB.config` file in the database repository, because they are listed in the `.gitignore` file). If you have changed some files and the pull does not work, you can use the command `git reset --hard` to reset all the changes you made inside the repository (again excepting locations in the `.gitignore` file) and then `git pull` again.
- **FYI:** The default configuration files `mangosd.conf.dist` and `realmd.conf.dist` will be overwritten during the update. If you changed them, make sure you changed their name or file type too (see [configuration](#configuration) section for more information).

### Released binaries

To update the precompiled binaries, go to the [release page on Github](#releases) and download a fresh copy of the zip file (the release is automatically updated when there are new commits). Extract the content of the zip file into your current server directory, overwriting existing files. Now you need to update your database. Occasionally database updates get delivered through the core repository instead of the DB repository. The script used later to do the database update will search the core repository for updates, if its path is provided in the `InstallFullDB.config` file (see [database filling](#filling) section).

### Self-compiled binaries

- In the Windows Explorer, navigate to `C:\mangos\mangos-VERSION\`.
- **Right-Click** and select **Git Bash Here**.
- Enter the `git fetch` command and wait until it is finished. It will look for updates in the repository on Github.
  
  ![update1](https://user-images.githubusercontent.com/8838573/27507706-d0d321ba-58d4-11e7-8771-8472ba7c6ba6.PNG)

- If there are updates on `origin/master`, enter the `git pull` command to download them.
  
  ![update2](https://user-images.githubusercontent.com/8838573/27507708-d901f672-58d4-11e7-8d8f-2ee7b31297c2.PNG)

- Redo the steps of the [Compilation](#compilation) section above.

### Database Update

- In the Windows Explorer, navigate to `C:\mangos\VERSION-db\`.
- **Right-Click** and select **Git Bash Here**.
- Enter the `git fetch` command and wait until it is finished. It will look for updates in the repository on Github.
  
  ![update3](https://user-images.githubusercontent.com/8838573/27507736-89811f1e-58d5-11e7-9f2c-8fe7bd6885b4.PNG)

- If there are updates on `origin/master`, enter the `git pull` command to download them.
  
  ![update4](https://user-images.githubusercontent.com/8838573/27507737-9234a464-58d5-11e7-8a20-accb73e47b9c.PNG)

- Enter the `./InstallFullDB.sh` command and wait until it is finished. The necessary `InstallFullDB.config` file should still be present and correctly set from installing.