These instructions are specific to MacOS 11. They were only tested with Mac OS X 11.1

## 1: Getting everything you need

**Privileges**

You must have access to an administrator account on your computer.

**Software tools**

In order to download, compile and install CMaNGOS and its tools, you will need the following software. All of them are free, though some may require you to register on the company website before downloading.

**Developers Tools (Xcode)**

You'll need them to compile the source files. They are provided to developers by Apple You can grab Xcode here: https://developer.apple.com/xcode/   
Don't forget to install the command line tools (Preferences>Download for the last version of Xcode)


**Homebrew**

Installation of many of the software packages below can be made much easier through use of a package manager.  The most popular package manager for MacOS is Homebrew, which is somewhat similar to e.g. the apt package manager in Debian/Ubuntu. Homebrew installation instructions and download can be found here: https://brew.sh/

**Boost lib**

The network part of CMaNGOS relies on the boost library. Install Boost with Homebrew with:
`$ brew install boost`

Alternatively, you can install/compile boost from http://www.boost.org/users/download/. We will assume that Boost is installed under `/usr/local/boost/`. You will need to let your OS know where Boost lib directory is by running:
```
$ echo "export DYLD_LIBRARY_PATH
$ DYLD_LIBRARY_PATH=/usr/local/boost/lib:DYLD_LIBRARY_PATH
$ export DYLD_LIBRARY_PATH
``` 

**MySQL Community Database Server**

Where a great part of the data about the game server side will be stored.  
Link: http://dev.mysql.com/downloads/mysql/?rz=gdl#downloads  
Of course, if you have a 64-bit Mac, install the 64-bit MySQL package

**Git**

Git comes with Xcode so you don't have to install it separately. If you want a newer version you can download it from http://git-scm.com/

**CMake**

To configure compilation. Get it from here: http://www.cmake.org/cmake/resources/software.html  
Of course, if you have a 64-bit Mac, install the 64-bit CMake package.

Once all these softwares are downloaded and installed on your Mac, you can move to the next step.

## 2. Building CMaNGOS - creating the world engine
From now, we will assume that:
* all the building will be done in a directory named mangos into your home directory
* you will download CMaNGOS sources into a subdirectory of this mangos folder (which we will also name mangos)
* you will install your server also into subdirectory of this mangos directory (which will be named run)
* your game client is located in /Applications/World of Warcraft/

First, we will download all sources for CMaNGOS and scripts.
Open Terminal and enter:
```
$mkdir mangos && cd mangos
$git clone git://github.com/cmangos/mangos-wotlk.git mangos
```
or for TBC:

`$git clone git://github.com/cmangos/mangos-tbc.git mangos`

Or for classic:

`$git clone git://github.com/cmangos/mangos-classic.git mangos`

Once the download is finished, we create the directory where the CMaNGOS server will be installed:

`$mkdir run`

Now, we will prepare to build the server

`$cd mangos`

Download the source files for the scripts (allows NPC to cast more spells and do complex things, not mandatory but you definitely want them):

`$git clone git://github.com/scriptdev2/scriptdev2.git src/bindings/ScriptDev2`

For TBC use instead:

`$git clone git://github.com/scriptdev2/scriptdev2-tbc.git src/bindings/ScriptDev2`

For Classic use instead:

`$git clone git://github.com/scriptdev2/scriptdev2-classic.git src/bindings/ScriptDev2`

We will now configure the compilation to tell cmake we want to install CMaNGOS server into the server directory we created earlier:

```
$mkdir build && cd build
$cmake .. -DCMAKE_INSTALL_PREFIX=~/mangos/run -DCMAKE_C_COMPILER=~/toolchains/gcc-4.8.5/bin/gcc -DCMAKE_CXX_COMPILER=~/toolchains/gcc-4.8.5/bin/g++ -DBOOST_INCLUDEDIR=/usr/local/boost/include
```

If everything is OK, we can compile:

`$make`

*Note: If your computer's CPU is multicore, you can instead type `$make -jN` where N is your number of cores. For instance, compiling on a 4 cores CPU: `$make -j4`
You can use the same command option everytime you will see `$make` in this tutorial.*

If everything went OK, we can install the compiled files:

`$make install`

Finally, we will create the config files from their template files.
```
$cd ~/mangos/run/etc/
$cp realmd.conf.dist realmd.conf
$cp mangosd.conf.dist mangosd.conf
$cp scriptdev2.conf.dist scriptdev2.conf
```

## 3. Extracting Maps and DBC - adding a world around the engine
Now the server is built and installed, we will extract all the maps, objects, spells and others data from the game files. The CMaNGOS server will need them to shape the world around your characters. The extractor utility is provided with the CMaNGOS source files and we will build it:
```
$cd ~/mangos/mangos
$cd ./contrib/extractor
$cmake -G "Unix Makefiles" -DCMAKE_OSX_ARCHITECTURES=i386
$make
```
There now should be an new file named `ad`. This is the Map/DBC Extractor. We will extract the maps and the DBC files from the game data and put the extracted files where the freshly compiled server was installed.
```
$cp ad /Applications/World\ of\ Warcraft/
$cd  /Applications/World\ of\ Warcraft/
$chmod +x ad
$./ad -f 0 -i /Applications/World\ of\ Warcraft/ -o .
```
You can either remplace `f 0` by `f 1`, depending of the accuracy you want for the maps (but at the cost of larger file size). You should now have two new directories: dbc and maps inside your WoW client folder. By default, they need to be put where the server binaires are. If you want to use mmaps (for pathfinding and smoother creatures movements), you can go to step 4. If you don't want to use mmaps, you can move the dbc and maps to the server directory:

`$mv dbc maps ~/mangos/run/bin/`
## 4. Installing the vmaps (optional, but highly recommended)
Vmaps are used by the server to determine if NPC can see/attack your characters, through walls for instance. This is also called LoS calculation (Line of Sight).
We will extract the vmaps from the game data and then assemble them. CMaNGOS does not yet provide binaries for Mac but it does provide the source files, thus we will build our own binaries. First, we need to download and apply a patch written by evil-at-wow and myself:

`$cd ~/mangos/mangos`

(copy paste the command line below into Terminal)
```
$curl https://gist.githubusercontent.com/cala/5784873/raw/0b06591d9aac800a2ede4b8ba4b15e586d5d789e/Fix%20extractors%20build%20for%20Mac%20OS%20X -o fix_extractors_for_os_x.patch
$git apply fix_extractors_for_os_x.patch
```
If everything went OK, you should not have any feedback and we need to commit (aka save the changes).

`$git commit -am "Fix extractors build for Mac OS X"`

Now the patch is applied, we can build the library allowing to extract from the game files:

```
$cd dep/libmpq/
$./autogen.sh
```
Some text will be displayed and should ends by `Now you are ready to run ./configure`. Let's do that:
```
$./configure CC="gcc -arch x86_64" CXX="g++ -arch x86_64" CFLAGS='-D_FILE_OFFSET_BITS=64 -D_LARGE_FILES=1 -D_LARGEFILE_SOURCE=1'
$make
```

The compilation should take a few minutes, then  we need to link the built library to the standard Mac OS X directory for third party libraries:
```
$ln -s /usr/local/lib/libmpq.4.0.2.dylib /Users/yourusername/mangos/mangos/dep/libmpq/libmpq/.libs/libmpq.4.0.2.dylib
$ln -s /usr/local/lib/libmpq.la /Users/yourusername/mangos/mangos/dep/libmpq/libmpq/libmpq.la
```
We are now ready to build the vmaps extractor/assembler:
```
$cd ../../contrib/vmapextractor/
$cmake -G "Unix Makefiles" -DCMAKE_OSX_ARCHITECTURES=x86_64
$make
```
When the compile process is done, a new file named vmapextractor should be in vmapextractor directory
We copy to our game client directory for later use:

`$cp vmapextractor/vmapextractor /Applications/World\ of\ Warcraft`

Now, let's build the vmap assembler:
```
$cd ../vmap_assembler/
$cmake -G "Unix Makefiles" -DCMAKE_OSX_ARCHITECTURES=x86_64
$make
```
When the compile process is done, a new file named vmap_assembler should be in the current directory. We need to copy it too to our game client directory:

`$cp vmap_assembler /Applications/World\ of\ Warcraft`

We can finally extract and assemble vmaps
```
$cd  /Applications/World\ of\ Warcraft
$chown +x vmap_assembler vmapextractor
```
Now, we create the directory where the vmaps will be extracted and we do the extraction:
```
$mkdir buildings
$./vmapsExtractor -d Data
```
This should take a few (dozen of) minutes. Once all the vmaps are extracted, we need to assemble them:
```
$mkdir vmaps
$./vmaps_assembler buildings vmaps
```
This will also take a few (dozen of) minutes. Once finished, we move the vmaps to the server repository and we clean the extracted data that we no longer need:
```
$mv vmaps ~/mangos/run/bin/
$rm -R buildings
```

## 5. Installing the mmaps (optional)
MovementMaps (mmaps) are used by the server to determine where a NPC can go (or not) with a fine precision: slopes, tree trunks, thin walls... It also enable the nice pathfinding with much better movement for creatures.  
We will extract the mmaps from the game data and previously extracted maps. CMaNGOS does not yet provide binary for Mac but it does provide the source files, thus we will build our own binary:
```
$cd ~/mangos/mangos/contrib/mmaps/
$cmake -G "Unix Makefiles" -DCMAKE_OSX_ARCHITECTURES=x86_64
$make
```
When the compile process is done, a new file named MoveMapGen should be in the current directory. We need to copy it too to our game client directory:

`$cp MoveMapGen MoveMapGen.sh /Applications/World\ of\ Warcraft`

We can finally extract the mmaps
```
$cd  /Applications/World\ of\ Warcraft
$chmod +x MoveMapGen*
```
Now, we create the directory where the mmaps will be generated:

`$mkdir mmaps`

And finally, we generated the mmaps (be aware that it will take hours, litteraly):

`$./MoveMapGen.sh N`

Where N is the number of core you want to use to extract the mmaps ranging from 1 to 4. 
Several hours later, when the mmaps are generated, we move them to the server binay folder, along with the maps and DBC:

`$mv dbc maps mmaps ~/mangos/run/bin/`


You have now complete all the steps that are specific to Mac OS X. For all the remaining steps (mainly configuration, database management and server startup), you can refer to the CMaNGOS Installation guide: https://github.com/cmangos/issues/wiki/Installation-Instructions

*Note: for MySQL, we advice using the very nice and free front end client: Sequel Pro http://www.sequelpro.com/*
