## Linux Core Enumeration Tools
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

## Windows Service Enumeration Tools
a) `Get-Service `( Powershell ) --> list all windows services with their name, display name and status. Used for quickly seeing waht services exists and which ones are active
b) `Get-WiniObject Win32_Service` ( Powershell ) --> Retrieves detailed service metadata form WMI, including executable path, service account, start mode, descriptiion and dependencies. This gives deeper information than Get-Service
c)` sc query` ( cmd ) --> Queries the Service Control Manager directly. It shows service state, PID, Type and exit codes. Used for low level service state inspection
d) `tasklist /svc` (cmd) --> Shows processes and the services running inside them
e)` net start` ( cmd ) --> LIsts only the services that are currently running. Fastest way to see active services without extra metadata
f) `wmic service list brief` ( cmd ) --> Legacy WMI interface. Shows a brief table of service name,state, start mode, display name. Useful for older windows systems
g) `Get-Process` ( Powershell ) -->  Lists all running process with PID, CPU/Memory usage and executable name. You use this to map process to a service with the help from tasklist /svc
h) `Get-NetTCPConnection` ( PowerShell ) --> shows active network connection with local/remote ports, state, owning process
i) Event viewer ( GUI ) --> provides service related logs including service failures, startup issues, crashes, permission problems. Clues are usually hidden in logs
j) Services.msc ( GUI ) --> For managing services. It shows the startup type, service account, Description and executable path. Useful for spotting suspicious or custom services visually
