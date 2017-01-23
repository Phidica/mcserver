# mcserver
An interactive Bash script to simplify the management of multiple Minecraft servers from a single unified location, including launching, backing up, and changing the message of the day (MotD; requires Python)

Current features:
* All servers (logs, world, and associated configuration files) are stored in separate directories, by default located in `~/.minecraft-server`
* All backups are stored in separate dated directories, by default located in `~/.minecraft-server/backups`
  * "backups" are just full copies of an entire server. The dated directory may contain backups of multiple servers for that day
* The server MotD may be viewed and changed prior to launch (requires Python)
* Prompts for backing up the server are presented when the server is stopped

Planned features:
* A new server can be created based on the template of an existing server, with level data imported from a custom location
* Implementation of noninteractive flags and arguments
* Interactive servers list sorted by date accessed, so default is most recent
* Extend `mcserver-motd` to handle all `server.properties` edits, especially to permit easy toggling of options such as command blocks

## Screenshots
![screenshot of directory tree](http://i.imgur.com/bnUIGwD.png)

Figure 1: Example of recommended main servers directory structure

## Requirements
The script requires the following packages and libraries:
* `python`
  * `sys`
  * `getopt`
  * `pyjavaproperties`

You may need to install `pyjavaproperties`:

    # pip install pyjavaproperties

## Installation
Clone the repository with

    $ git clone https://github.com/Phidica/mcserver.git

Copy the `mcserver` and `mcserver-motd` files to your directory of choice. `~/.local/bin/` is a good one, if that's on your `$PATH`. Make the primary script executable with

    $ chmod +x mcserver

Edit the `mcserver` file, if necessary, to ensure it points to an existing main servers directory containing more directories where each consists of the components for one server

Server directory names cannot contain whitespace or particularly fancy characters

Each server directory must contain a `run.sh` script that will cause that server to start. An example of a valid `run.sh` script is the following:

    java -Xms2G -Xmx4G -jar ../minecraft_server.1.8.8.jar nogui

Note that the implication here is that the main servers directory contains server JAR files, as seen in Figure 1, which is recommended to keep them out of the backups. If you wish to keep the server JAR in the server directory, do so and remove the `../` from the example above

## Execution
The primary program accepts no flags or arguments, just run:

    $ mcserver