# Linux Command Line & Directory Structure Cheat Sheet

## 🔹 Working With the Command Line

-   **who** -- shows logged-in users\
-   **whoami** -- shows your current username\
-   **id** -- displays user ID and group info\
-   **groups** -- lists groups current user belongs to\
-   **finger** -- detailed info about users\
-   **w** -- shows who's logged in and what they're doing\
-   **last** -- login history\
-   **lastb** -- failed login attempts\
-   **lastlog** -- last login of all users\
-   **users** -- logged-in usernames\
-   **uptime** -- system uptime and load\
-   **hostname** -- system's hostname\
-   **hostnamectl** -- system hostname + OS details\
-   **lscpu** -- CPU architecture details\
-   **lshw** -- detailed hardware info\
-   **free** -- memory usage\
-   **df** -- disk usage (by filesystem)\
-   **du** -- disk usage (by directory/file)\
-   **top** -- running processes (real-time)\
-   **htop** -- interactive process viewer (improved `top`)\
-   **ps** -- process snapshot\
-   **pstree** -- processes in tree view\
-   **kill** -- kill process by PID\
-   **pkill** -- kill process by name\
-   **nice** -- start process with priority\
-   **renice** -- change priority of a running process\
-   **bg** -- resume job in background\
-   **fg** -- bring job to foreground\
-   **jobs** -- list background jobs\
-   **tty** -- terminal device name\
-   **date** -- show system date & time\
-   **cal** -- show calendar\
-   **runlevel** -- shows current runlevel\
-   **uname -r** -- kernel version\
-   **uname -a** -- system info (all)\
-   **ifconfig** -- network configuration\
-   **history** -- command history\
-   **! 25** -- run command #25 from history\
-   **history -c** -- clear command history

------------------------------------------------------------------------

## 🔹 Shutting Down and Rebooting

-   **init 0** -- shutdown\
-   **poweroff** -- power off\
-   **shutdown -h now** -- halt immediately\
-   **shutdown -h 10** -- halt in 10 minutes\
-   **shutdown -h 10 "msg"** -- halt in 10 mins with message\
-   **shutdown -c** -- cancel scheduled shutdown\
-   **init 6** -- reboot\
-   **reboot** -- restart immediately\
-   **shutdown -r now** -- reboot immediately\
-   **shutdown -r 10** -- reboot in 10 minutes\
-   **shutdown -r 10 "msg"** -- reboot in 10 mins with message

------------------------------------------------------------------------

## 🔹 Linux Directory Structure

-   **/** -- root directory\
-   **/bin** -- user binaries (executables)\
-   **/boot** -- boot loader files\
-   **/dev** -- device files (USB, HDD, etc.)\
-   **/etc** -- configuration files\
-   **/home** -- user home dirs\
-   **/lib** -- system libraries\
-   **/media** -- removable media mount point\
-   **/mnt** -- temporary mount point\
-   **/opt** -- optional software\
-   **/proc** -- process/system info (virtual fs)\
-   **/root** -- root user's home\
-   **/run** -- runtime service info\
-   **/sbin** -- system binaries (admin use)\
-   **/srv** -- service data (FTP, HTTP, etc.)\
-   **/sys** -- system info (hardware)\
-   **/tmp** -- temporary files\
-   **/usr** -- user apps & packages\
-   **/var** -- variable data (logs, cache, spool)
