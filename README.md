# Minecraft C Shell
C Shell scripts for Minecraft dedicated servers, based on a RCON reimplementation.

#### Scripts descriptions
*rcon_announce*: Periodically display a set of three messages after five minutes + two other messages, after 30 seconds, counted from the five minutes.\
*rcon_commands*: Execute commands requested by a player; currently, the commands are: !date (*date* Unix command), !info (*uname -a* Unix command), !script (script information; credits), !warp (manage warps) and !guild (manage guilds).\
*rcon_auth*: Authenticate players, basing on usernames and IP addresses.

#### How to use
Do not have the server running, change the scripts' execution permissions and run the following:\
`mkfifo /tmp/rcon_in ; tail -f /tmp/rcon_in | java -jar <path/to/server.jar> server nogui &`\
`tail -f <path/to/server.jar/logs/latest.log> | ./rcon_auth" &`\
`tail -f <path/to/server.jar/logs/latest.log> | ./rcon_commands" &`\
`./rcon_announce &`\
To enable external RCON connections, install [socat](http://www.dest-unreach.org/socat) and do the following:\
(For logs.) `socat -U tcp-l:<port>,fork,reuseaddr exec:"tail -f <path/to/server.jar/logs/latest.log>" &`\
(For commands.) `( nc -p<port> -kl > /tmp/rcon_in & )`\
To have RCON access, do the following:\
(For logs.) `nc <server ip> <port> &`\
(For commands.) `echo <command> | nc <server ip> <port>`

#### Notes
Windows users may use [Cygwin](https://cygwin.com) to run the scripts.

Because Minecraft's RCON is terrible, I had to implement one, with a FIFO (first in, first out).

The scripts should work on both original and CraftBukkit/Spigot servers.

On Unix and Unix-like operating systems, it is recommended to have a `tmpfs` mount on `/tmp`.
