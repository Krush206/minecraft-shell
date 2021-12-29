# Minecraft C Shell
C Shell scripts for Minecraft dedicated servers, based on a RCON reimplementation.

#### Scripts descriptions
*rcon_announce*: Periodically display a set of three messages after five minutes + two other messages, after 30 seconds, counted from the five minutes.\
*rcon_commands*: Execute commands requested by a player; currently, the commands are: !date (*date* Unix command), !info (*uname -a* Unix command), !script (script information; credits), !warp (manage warps) and !guild (manage guilds).\
*rcon_auth*: Authenticate players, basing on usernames and IP addresses.

#### How to use
Do not have the server running, install [socat](http://www.dest-unreach.org/socat), change the scripts' execution permissions and run the following:\
`tail -f rcon_in | java -jar <path/to/server.jar> server nogui &`\
`socat -u exec:"tail -f <path/to/server.jar/logs/latest.log>",crnl exec:"./rcon_auth" &`\
`socat -u exec:"tail -f <path/to/server.jar/logs/latest.log>",crnl exec:"./rcon_commands" &`\
`./rcon_announce &`\
To enable external RCON connections, do the following:\
(For logs.) `socat -U tcp-l:<port>,fork,reuseaddr exec:"tail -f <path/to/server.jar/logs/latest.log>" &`\
(For commands.) `( nc -p<port> -kl > rcon_in & )`\
To have RCON access, do the following:\
(For logs.) `nc <server ip> <port> &`\
(For commands.) `echo <command> | nc <server ip> <port>`

#### Notes
Still need to port rcon_auth.

Windows users may use [Cygwin](https://cygwin.com) to run the scripts.

Because Minecraft's RCON is terrible, I had to implement one, with a FIFO (first in, first out).

The scripts should work on both original and CraftBukkit/Spigot servers.
