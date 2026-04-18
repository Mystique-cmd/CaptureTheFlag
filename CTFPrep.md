Linux Core Enumeration Tools
a) `systemctl list-units --type=service` --> Shows all active systemd services currently loaded and recognized by the OS
b)` systemctl status <service>` --> Shows the full status of a specific service. This is where you spot misconfigurations or unusual behavior
c)` service --status-all `--> List all services including older non systemd ones. Useful in older systems or mixed environments
d) `ps aux` --> Lists all running processes with details
e) `ss -tulnp` --> Show active network sockets ( TCP/UDP) with listening ports, associated PIDs and protocols. Tells which  services are exposed on the network.
f) `netstat - tulnp `--> Older version ss. Used when ss in unavailable
g) `journalctl -u <service>` --> Shows the logs for a specific service. It is critical for spotting : startup errors, crashes, custom scripts, suspicious behaviours.
h)` lsmod`--> Lists loaded kernel modules. Useful for identifying drivers, kernel extensions, unusual modules
i) `lsof -i` --> Lists open network connections by process. More detailed than ss becaue it shows file descriptors, exact binary path, user
j) /etc/services --> a static file mapping port numbers to service names. Usefule for quick reference.
k) /etc/systemd/system/ --> Directory containinig custom systemd service unit files. This si where CTFs often hide: flags, custom scripts, weird ExecStart commands
l) /etc/init.d/ --> Check here when a service does not appear in systemd.
