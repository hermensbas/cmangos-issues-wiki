# Running CMaNGOS as a systemd service

If you are on Linux and use systemd as your init system (default on most popular distributions) you can write [unit configuration files](https://www.freedesktop.org/software/systemd/man/systemd.service.html) to let systemd handle starting your cmangos server as a background process called a service.

Below you will find two example files to start the cmangos world and login servers.

## File locations

We assume you have your cmangos configuration files in the default directories relative to the binaries, `/path/to/cmangos/etc/` and `/path/to/cmangos/bin/` respectively, where `/path/to/cmangos/` is the installation location you chose during compilation.

You should also have removed the `.dist` ending from the configuration files, so the binaries will automatically find them. If this isn't the case you will have to manually supply their location (see comments in the example files below).

## Disabling the world servers interactive console

You have to disable the server console of `mangosd`. **This is important! If you don't disable the console the service won't work.** Open your `mangosd.conf`, search for the line `Console.Enable = 1` and change it to `0`.

If you don't want to change the default config file so you still have the console when starting from the terminal, you can copy the config file to another name and supply its path to `mangosd` with the `-c` option (see below).

## The world server

You have to create a file in the `/etc/systemd/system` directory or link it to there.

You can choose its name freely as long as it ends in `.service`, it will become the name the `systemctl` command uses. E.g. if the file is named `mangosd-classic.service` you will be able to start the service with `systemctl start mangosd-classic`.

Create the file, copy this text and then replace all occurences of `/path/to/cmangos/` with your installation location.

If you are not using the `mangos` user on your system, you will have to change the `User=mangos` line as well.

```
[Unit]
Description=CMaNGOS world server
After=network.target
Requires=mysqld.service
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=always
RestartSec=1

# Set your username here if it differs
User=mangos
# Set your install location here
WorkingDirectory=/path/to/cmangos/bin
# And here
ExecStart=/path/to/cmangos/bin/mangosd

# Example with the config options manually passed along:
# ExecStart=/path/to/cmangos/bin/mangosd -c /path/to/cmangos/etc/mangosd.conf -a /path/to/cmangos/etc/ahbot.conf -p /path/to/cmangos/etc/playerbot.conf

[Install]
WantedBy=multi-user.target
```

## The realm server

The file for the realm server looks basically exactly the same, but with a different name and different pathes of course. It also only accepts the `-c` option, `-a` and `-p` are not required for the `realmd` binary.

```
[Unit]
Description=CMaNGOS login server
After=network.target
Requires=mysqld.service
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=always
RestartSec=1

User=mangos
WorkingDirectory=/path/to/cmangos/bin
ExecStart=/path/to/cmangos/bin/realmd
# ExecStart=/path/to/cmangos/bin/realmd -c /path/to/cmangos/etc/realmd.conf

[Install]
WantedBy=multi-user.target
```

## Activating the service files

To make systemd aware of the new files you need to run `sudo systemctl daemon-reload`. This is also applies if you add changes to the files later.

## Using the services

There are several subcommands of `systemctl` that you can use to manage your services. Assuming you named your files `mangosd-classic.service` and `realmd-classic.service` you would start them like this:

```
$ sudo systemctl start mangosd-classic
$ sudo systemctl start realmd-classic
```

When you do a `systemctl status <service>` command (no `sudo` needed for this one) you should see a line like this somewhere at the top:

```
Active: active (running) since ...
```

If it doesn't, something went wrong.

You can stop them like this:

```
$ sudo systemctl stop mangosd-classic
$ sudo systemctl stop realmd-classic
```

Since the script sets the `Restart=always` option, the server will always restart if it crashes. But after a system reboot the service will not start on its own again. If you want them to start automatically on boot, you will have to use the `enable` and `disable` subcommands of `systemctl` instead of `start` and `stop`:

```
$ sudo systemctl enable mangosd-classic
$ sudo systemctl enable realmd-classic
```