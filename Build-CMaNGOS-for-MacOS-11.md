**These instructions are specific to MacOS 11 and were only tested with Mac OS X 11.1**

**Privileges**

We must have access to an administrator account on your computer. Nearly all steps will be carried out via Terminal.


## 1: Software Tools

In order to download, compile and install CMaNGOS and its tools, we will need the following free software:


**Developers Tools (Xcode)**

This is what we will use to compile the source files. Provided to developers by Apple, you can find Xcode here: https://developer.apple.com/xcode/   
**Don't forget to install the Xcode Command Line Tools!**


**Homebrew**

Installation of many of the software packages below can be made much easier through use of a package manager. The most popular package manager for MacOS is Homebrew, which is somewhat similar to e.g. the apt package manager in Debian/Ubuntu. Homebrew installation instructions can be found here: https://brew.sh/

**Most of the installation instructions that follow are carried out via Terminal.**


**Boost lib**

The network part of CMaNGOS relies on the Boost library. We can install Boost with Homebrew:
`$ brew install boost`

Boost libraries should be found in the directory `/usr/local/opt`. If they are not, we must copy them to this location. Homebrew may install boost in `/usr/local/Cellar`, so look there first.

We will also need to let MacOS know where the Boost libraries reside. We can save the path to and reload our zsh profile by executing the following commands:
```
$ echo "export DYLD_LIBRARY_PATH=/usr/local/opt/boost/lib:DYLD_LIBRARY_PATH" >> ~/.zshrc"
$ source ~/.zshrc
``` 


**MySQL Community Database Server**

A great part of the game server data will be stored using MySQL. Currently, version <=5.7 of MySQL is supported.

We can install the proper version of MySQL with:
`$ brew install mysql@5.7`


**Git**

Git comes with Xcode, so it needn't be installed separately. The official git website is http://git-scm.com/


**CMake**

CMake configures our Makefiles, which are in turn used to compile our code. We can install CMake with:
`$ brew install cmake`


Once this software is installed, we can move to the next step.



## 2. CMaNGOS Build Setup

The following is a brief overview of the directory structure we will assume for this project (step-by-step instructions follow):
* The entire CMaNGOS application will reside in a project folder named `mangos`
* We will download CMaNGOS source code into a subdirectory of the `mangos` project folder, named `mangos-wotlk`
* We will install the server application into subdirectory of `mangos` named `run`
* The World of Warcraft game client is located at /Applications/World of Warcraft/

**Clone the CMaNGOS and ScriptDev Repositories**
First, we will download or "clone" the source code repository for CMaNGOS. We have chosen to create our `mangos` project directory in our home directory (i.e. `/Users/<username>/`), but the `mangos` project can be placed anywhere we have appropriate read/write/execute privileges. Our home directory is the safest bet. Note that the tilde `~` can be used in place of the home directory path, i.e. `/Users/<username>/mangos` is the same as writing `~/mangos`.

From Terminal, we execute the following. This may take a few moments:
```
$ cd ~
$ mkdir -p mangos/run && cd mangos
$ git clone git://github.com/cmangos/mangos-wotlk.git
```

Next, we clone the ScriptDev repository. ScriptDev allows NPC to cast more spells and do complex things. This not mandatory but we will certainly want it:

`$ git clone git://github.com/scriptdev2/scriptdev2.git mangos-wotlk/src/bindings/ScriptDev2`

For TBC use instead:

`$ git clone git://github.com/scriptdev2/scriptdev2-tbc.git mangos-tbc/src/bindings/ScriptDev2`

For Classic use instead:

`$ git clone git://github.com/scriptdev2/scriptdev2-classic.git mangos-classic/src/bindings/ScriptDev2`

## 3. Build and Install (Create the engine)

We will now compile our application

```
$ mkdir build && cd build
$ cmake ../mangos-wotlk -DCMAKE_INSTALL_PREFIX=\../mangos/run -DBUILD_EXTRACTORS=ON -DPCH=1 -DDEBUG=0
```

If we've made it this far, we're ready to build:

`$ make`

If successful, we can install the compiled files:

`$ make install`


## GUIDE TESTED TO HERE



Finally, we will create the config files from their template files.
```
$ cd ~/mangos/run/etc/
$ cp realmd.conf.dist realmd.conf
$ cp mangosd.conf.dist mangosd.conf
```

## 4. Extract Maps and DBC (Add a world around the engine)
Now that the server is built and installed, we will extract all the maps, objects, spells and others data from the game files. The CMaNGOS server will need them to shape the world around our characters. The extractor utility can be built from the CMaNGOS source files:
```
$ cd ~/mangos/mangos-wotlk/contrib/extractor
$ cmake -G "Unix Makefiles"z
$ make
```
There now should be an new file named `ad`. This is the Map/DBC Extractor. We will extract the maps and the DBC files from the game data and put the extracted files where the freshly compiled server was installed. Note that we can replace `f 0` by `f 1` on the last line for more accurate maps, but at the cost of larger file size).
```
$ cp ad /Applications/World\ of\ Warcraft/
$ cd /Applications/World\ of\ Warcraft/
$ chmod +x ad
$ ./ad -f 0 -i /Applications/World\ of\ Warcraft/ -o .
```
We should now have two new directories inside our World of Warcraft client folder: dbc and maps. By default, these folders need to be located with the server binaires we built in step 4. If we want to use mmaps (for pathfinding and smoother creatures movements), we can continue to step 5. Otherwise, we simply move the dbc and maps folders to the server directory:

`$ mv dbc maps ~/mangos/run/bin/`


## 5. Installing the vmaps (optional, but highly recommended)
Vmaps are used by the server to determine if an NPC can see/attack our characters, through walls for instance. This is also called LoS calculation (Line of Sight).
We will extract the vmaps from the game data and then assemble them. CMaNGOS does not yet provide binaries for Mac but it does provide the source files, thus we will build our own binaries. First, we need to download and apply a patch written by evil-at-wow and cala:

`$ cd ~/mangos/mangos-wotlk`

(copy paste the command line below into Terminal)
```
$ curl https://gist.githubusercontent.com/cala/5784873/raw/0b06591d9aac800a2ede4b8ba4b15e586d5d789e/Fix%20extractors%20build%20for%20Mac%20OS%20X -o fix_extractors_for_os_x.patch
$ git apply fix_extractors_for_os_x.patch
```


## GUIDE UPDATED TO HERE


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
