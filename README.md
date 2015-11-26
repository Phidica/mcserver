# mcserver
A collection of Bash and Python scripts to simplify the management of multiple Minecraft servers from a single unified location

Current features:
* All servers (logs, world, and associated configuration files) are stored in separate directories, by default located in *~/.minecraft-server*
* All backups are stored in separate dated directories, by default located in *~/.minecraft-server/backups*
  * "backups" are just full copies of an entire server. The dated directory may contain backups of multiple servers for that day
* The server message of the day (MotD) may be viewed and changed prior to launch
* Prompts for backing up the server are presented when the server is stopped

Planned features:
* Ability to create a new server from a blank template, and populate the world with data from a chosen directory

## Requirements
The script requires the following packages and libraries:
* python
  * sys, getopt, pyjavaproperties

You may need to install pyjavaproperties:

    $ pip install pyjavaproperties

## Installation
Clone the repository with

    $ git clone https://github.com/Rhotias/mcserver.git

Copy the *mcserver* and *mcserver-motd* files to your directory of choice. *~/.local/bin/* is a good one, if that's on your $PATH. Make the primary script executable with

    $ chmod +x mcserver

Edit the *mcserver* file if necessary to ensure it points at an existing servers directory containing more directories where each consists of the components for one server

Each directory must contain a *run.sh* script that will cause that server to start. An example of a valid *run.sh* script is the following:

    java -Xms2G -Xmx4G -jar ../minecraft_server.1.8.8.jar nogui

Note that the implication here is that the main servers directory contains server JAR files, which is recommended to keep them out of the backups. If you wish to keep the server JAR in the same directory as the server itself, do so and remove the *../* from the example above

## Execution
The primary program accepts no flags or arguments, just run:
    mcserver