FlatacraftBanManagement
=======================

New Website updated with bans on the servers on our network
------------------------

n advanced SQL based ban management system for your server which allows you to store reasons for bans

Managing a server can be quite difficult, let alone multiple servers with multiple staff. We at Frostcast were getting lots of posts on our forums from people who were asking to be unbanned. The amount of time it took having to find out who banned them and why was too long. Ban management was born.

Ban management stores all bans in a MySQL database. Not only does it tell you why they were banned, but by who and the time that they were banned at. Upon the banned player trying to login to the server, the reason is shown. If it is a tempban, it shows the time left until they can join again.

It also uses Bukkit's inbuilt banning system. If the MySQL database ever fails or is inaccessible, it has that to fall back on. This plugin does NOT take into account bans via bukkit prior to the plugin installation

The plugin also keeps a record of all previous bans in the database, so previous banning can be taken into account when dealing with certain players.
Web-based Frontend

Installation Instructions

This plugin provides a PHP script which allows you to view all data created with the plugin as well as edit/remove bans, mutes and warnings.

It connects to the database where the data is stored and presents it in an easy to view format.

This script makes use of a file based cache system to prevent MySQL abuse. All searches and player views are cached for 5mins. Server statistics are stored for an hour.

Search % to show a list of all players.

Demo: http://www.frostcast.net/banmanagement/
Usage

/ban <username> <reason>
/tempban <username> <timeFormat> <reason>
/unban <username>
/bminfo <username>
/banip <username || IP> <reason>
/tempbanip <username || IP> <timeDiff> <reason>
/unbanip <ip>
/banimport <player || ip> <default reason> Example: /banimport player Unknown
/kick <player> <reason (optional)>
/nlkick <player> <reason (optional)> (If kick logging enabled, using this command will force the kick not to be logged)
/mute <username> <reason>
/tempmute <username> <timeFormat> <reason>
/unmute <username>
/warn <username> <reason>
/bmreload

Time Format

    10s = 10 seconds
    10m = 10 minutes
    10h = 10 hours
    10d = 10 days
    10mo = 10 months
    10y = 10 years 

Example: /tempban player 1y2m spamming, swearing & hacking

Permissions

    bm.ban - Allows a player to permanently ban someone.
    bm.tempban - Allows a player to tempban someone.
    bm.unban - Allows a player to unban someone.
    bm.exempt.kick - Players with this permission cannot be kicked, highly recommended for admins.
    bm.exempt.ban - Players with this permission cannot be banned, highly recommended for admins.
    bm.exempt.tempban - Players with this permission cannot be temporarily banned,highly recommended for admins.
    bm.exempt.mute - Players with this permission cannot be muted, highly recommended for admins.
    bm.exempt.tempmute - Players with this permission cannot be temporarily muted, highly recommended for admins.
    bm.exempt.banip - Players with this permission cannot be ip banned, highly recommended for admins.
    bm.notify - Players with this permission are notified when a player is banned.
    bm.bminfo - Allows use of /bminfo which shows a players current ban info.
    bm.banip - Allows you to ban an ip.
    bm.tempbanip - Allows you to tempban an ip.
    bm.unbanip - Allows you to unban an ip.
    bm.import - Allows importing of banned players and ips from Bukkit.
    bm.kick - Allows you to kick another player.
    bm.update - Notifies the player if an update for the plugin is available.
    bm.mute - Allows you to mute a player.
    bm.tempmute - Allows you to temp mute a player.
    bm.unmute - Allows you to unmute a player.
    bm.reload - Allows you to reload from the config.
    bm.timelimit.bans.bypass - Allows you to bypass any group limitations on temporary ban lengths.
    bm.timelimit.mutes.bypass - Allows you to bypass any group limitations on temporary mute lengths.
    bm.warn - Allows you to warn a player.
    bm.banoffline - Required to permanently ban an offline player, bm.ban is still required.
    bm.tempbanoffline - Required to temban an offline player, bm.tempban is still required. 

Installation

    Stop the server
    Add the .jar file to /plugins
    Start the server, the config file will be generated. An error will show upon start up, this is normal.
    Stop the server
    Modify the config file with your database details, you do not have to create the tables, the plugin will do that for you
    If you run multiple minecraft servers from 1 database each of them running this plugin and you do not want the bans to sync across them all, you can change the table names in the config file.
    Start the server
    Errors on start up mean you have entered your MySQL details incorrectly 

3306 is the default MySQL port
Config

See here.
FAQ

When adding my server to the web interface, it says tables not found

    Ensure you run the plugin first before the web interface. The plugin creates the tables for you. If it still says tables not found, double check the tables in the config.yml and make sure they are what you are inputting into the web interface. 

When adding my server to the web interface, it says Unable to connect

    Ensure your connection details are correct. If they are, your MySQL database is probably refusing remote access. Grant the IP of your web server permission to access the database. If you are unsure of how to do this, ask your mysql server host. If you are on a dedicated server, ssh in and run the following queries as root to grant access, replacing dbname with the name of your database, username with the username you want to use to connect to the database, IP with the ip address of the web server and finally, the password for the username. 

GRANT ALL PRIVILEGES ON dbname.* TO username@'IP' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;

Can I edit the web interface to fit in with my sites theme?

    Yes you can edit the web interface to your liking. All that I ask is the copyright notice and link back to Frostcast remains untouched. If you find anyone failing to comply, please PM me. 

Can I use colours in the custom messages?

    Yes you can. Simply use & followed by the corresponding colour number. For example &c for red, or &6 for gold. A full list of colours can be found here. 

Can I separate the ban message shown to banned players on to different lines?

    Yes, simply use \n within the message in the config.yml wherever you'd like a new line to start. 

Can I sync bans across all my servers?

    Absolutely. Simply use the same MySQL database and tables for each config. If you wish to see which server the ban was issued on, simply set a different serverName in the config for each server. 

Can I import bans from my banned-players.txt and banned-ips.txt files?

    Yes using the /banimport command. If you want to import players then use /banimport player followed by the default reason you wish them all to be banned for. For example '/banimport player I have no idea' will import all players from banned-players.txt and set their ban reason to 'I have no idea'. For ips, its exactly the same except type ip instead of player. 

Can I limit the amount of time certain players or groups can temp ban or temp mute someone?

    Yes, look in the config at the node timeLimits. By default you'll see moderator. Any group and or person with the permission bm.timelimit.bans.Moderator can only tempban someone for a day, and bm.timelimit.mutes.Moderator for 1 hour. You can create as many groups as you like and customise the time limits however you like, they use the same format as the timeFormat option in /tempban and /tempmute. Players still need the permissions bm.tempban to temp ban and bm.tempmute to temp mute. 

On start-up I get an error 'Unsupported major.minor version 51.0'

    Update to Java 7. If you still are on Java 6 you should really update, the performance gains are noticeable. 

On start-up I get an error 'Error occurred while enabling BanManager vX (Is it up to date?) java.lang.NullPointerException at me.confuserr.banmanager.BanManager.onEnable(BanManager.java:212)'

    This is an issue with CommandBook who refuse to fix it. Possible fix by @xpopy is 'Changing "low-priority-command-registration:" to "true" in CommandBook fixes the error message.' 

API

Simply add the plugin to your build path and call the class BmAPI.
Source

GitHub
Supporters

The following sites have permission to remove the attribution notice:

    cursecraft.net
    lava-craft.net
    minenation.net
    cowcraft.net 

To Do's

    Ban Appeal System 

Known Issues

    Web interface doesn't always allow you to login. Some sort of session conflict with other scripts. Try logging out of other things on your website. 

Metrics

