# Minecraft Shell
Shell (Bash) scripts for Minecraft dedicated servers.

#### Scripts descriptions
*rcon_announce*: Periodically display a set of three messages after five minutes + two other messages, after 30 seconds, counted from the five minutes.\
*rcon_commands*: Execute commands requested by a player; currently, the commands are: !date (*date* Unix command), !info (*uname -a* Unix command), !script (script information; credits) and !give (give the requested item by a player).

#### How to use
Do not have the server running, install [socat](http://www.dest-unreach.org/socat), change the scripts' execution permissions and run the following:\
`nc -Ukl rcon_in | java -jar <path/to/server.jar> nogui | tee -a rcon_log | nc -Ukl rcon_out &`\
`socat -u unix:rcon_out,reuseaddr exec:"./rcon_commands"`\
`./rcon_announce`

#### Notes
Since I made them on GNU/Linux, it is unlikely that Unix or other Unix-like operating systems (including macOS) be able to run them, because GNU programs tend to be and act different than these found in Unix and other Unix-like operating systems. However, *BSD and illumos users may already have or can install GNU programs, so they just need to adapt their environment.

Even though the above is true, I'm writing the scripts with POSIX in mind.

Windows users may use [Cygwin](https://cygwin.com) to run the scripts.

Because Minecraft's RCON is terrible, I had to implement one, with Unix domain sockets.

Server logs are outputted to and can be seen in the `rcon_log` file.

The scripts should work on both original and CraftBukkit/Spigot servers.
