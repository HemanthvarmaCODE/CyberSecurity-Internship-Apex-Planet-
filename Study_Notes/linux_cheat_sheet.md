# Linux Commands Cheatsheet

A comprehensive reference guide for essential Linux commands covering file system navigation, permissions, package management, and networking.

---

## File System Navigation

### pwd (Print Working Directory)

Displays the full pathname of the current working directory.

```bash
pwd
```

**Output example:**
```
/home/username/Documents
```

---

### ls (List)

Lists files and directories in the current directory.

**Basic usage:**
```bash
ls
```

**List all files including hidden files:**
```bash
ls -a
```

**List in long format (detailed information):**
```bash
ls -l
```

**Combine options:**
```bash
ls -la
```

**List with human-readable file sizes:**
```bash
ls -lh
```

**List directories only:**
```bash
ls -d */
```

**List recursively (including subdirectories):**
```bash
ls -R
```

**Sort by modification time (newest first):**
```bash
ls -lt
```

**Sort by file size (largest first):**
```bash
ls -lS
```

**Common output format explanation:**
```
-rw-r--r-- 1 user group 1234 Jan 1 12:00 filename
│││││││││  │ ││││ ││││  ││││ └─────┬─────┘ └──┬───┘
│││││││││  │ ││││ ││││  └─size    modified   name
│││││││││  │ ││││ └─group
│││││││││  │ └─owner
│││││││││  └─hardlinks
└─permissions
```

---

### cd (Change Directory)

Changes the current working directory.

**Change to a specific directory:**
```bash
cd /path/to/directory
```

**Change to home directory:**
```bash
cd
```

**or:**
```bash
cd ~
```

**Change to previous directory:**
```bash
cd -
```

**Change to parent directory:**
```bash
cd ..
```

**Change to parent directory multiple levels:**
```bash
cd ../../
```

**Change to root directory:**
```bash
cd /
```

**Use absolute path:**
```bash
cd /home/username/Documents
```

**Use relative path:**
```bash
cd ./subfolder
```

---

### Other Navigation Commands

**pwd with logical vs physical:**
```bash
pwd -L    # Logical path (with symlinks)
pwd -P    # Physical path (actual location)
```

**pushd and popd (Directory stack):**
```bash
pushd /path/to/directory    # Change directory and save current to stack
popd                         # Return to previous directory from stack
dirs                         # View directory stack
```

---

## File & Directory Permissions

### Understanding Permission Format

```
-rw-r--r--
│││││││││
│└┴┴ Owner  (user)
│   └┴┴ Group
│       └┴┴ Others
└ File type (- = file, d = directory, l = link)
```

**Permission values:**
- `r` (read) = 4
- `w` (write) = 2
- `x` (execute) = 1

---

### chmod (Change Mode)

Changes file or directory permissions.

**Using symbolic notation:**
```bash
chmod u+x filename              # Add execute permission for owner
chmod u-w filename              # Remove write permission for owner
chmod g+r filename              # Add read permission for group
chmod o-r filename              # Remove read permission for others
chmod a+r filename              # Add read permission for all
chmod u=rwx,g=rx,o= filename   # Set specific permissions
```

**Using numeric notation:**
```bash
chmod 644 filename              # rw-r--r-- (owner: read+write, group: read, others: read)
chmod 755 directory             # rwxr-xr-x (owner: all, group: read+execute, others: read+execute)
chmod 700 privatefile           # rwx------ (owner: all, others: none)
chmod 777 filename              # rwxrwxrwx (everyone: all permissions)
chmod 600 secretfile            # rw------- (owner: read+write, others: none)
chmod 444 readonly              # r--r--r-- (everyone: read only)
```

**Recursive permission change:**
```bash
chmod -R 755 directory          # Change permissions for directory and all contents
chmod -R u+w directory          # Add write permission recursively for owner
```

**Common permission combinations:**
```bash
chmod 644 *.txt                 # Apply to multiple files
chmod -R 755 ./public_html      # Typical for web directories
chmod -R 700 ./private          # Private directory with no group/others access
chmod u+x script.sh             # Make script executable for owner
```

---

### chown (Change Owner)

Changes the owner and/or group of files or directories.

**Change owner only:**
```bash
chown newowner filename
```

**Change group only:**
```bash
chown :newgroup filename
```

**Change both owner and group:**
```bash
chown newowner:newgroup filename
```

**Recursive change (directory and all contents):**
```bash
chown -R newowner directory
chown -R newowner:newgroup directory
```

**Preserve links (don't follow symbolic links):**
```bash
chown -h newowner filename
```

**Verbose output (shows what's being changed):**
```bash
chown -v newowner filename
chown -vR newowner:newgroup directory
```

**Common examples:**
```bash
sudo chown user:user myfile              # Change to user's ownership
sudo chown -R www-data:www-data /var/www # Web server directory
chown root:root configuration.conf        # System configuration file
```

---

### Viewing Permissions

**Check permissions of a file:**
```bash
ls -l filename
```

**Check permissions of a directory:**
```bash
ls -ld directory
```

**Check permissions recursively:**
```bash
ls -lR directory
```

**Check current user and groups:**
```bash
whoami                          # Current user
groups                          # Groups of current user
id                              # User ID and group IDs
```

**Convert numeric permission to symbolic:**
```bash
chmod 755 = rwxr-xr-x
chmod 644 = rw-r--r--
chmod 700 = rwx------
chmod 600 = rw-------
chmod 777 = rwxrwxrwx
chmod 400 = r--------
```

---

## Package Management

### apt (Advanced Package Tool)

Primary package manager for Debian/Ubuntu systems.

**Update package lists:**
```bash
sudo apt update
```

**Install a package:**
```bash
sudo apt install package-name
```

**Install multiple packages:**
```bash
sudo apt install package1 package2 package3
```

**Upgrade all installed packages:**
```bash
sudo apt upgrade
```

**Full upgrade (dist-upgrade):**
```bash
sudo apt full-upgrade
```

**or:**
```bash
sudo apt dist-upgrade
```

**Remove a package (keeps configuration files):**
```bash
sudo apt remove package-name
```

**Remove a package completely (removes configuration files):**
```bash
sudo apt purge package-name
```

**Search for a package:**
```bash
apt search search-term
```

**Show package information:**
```bash
apt show package-name
```

**List installed packages:**
```bash
apt list --installed
```

**List upgradeable packages:**
```bash
apt list --upgradeable
```

**Clean up old cache and dependencies:**
```bash
sudo apt clean                  # Remove cache files
sudo apt autoclean              # Remove old cache files only
sudo apt autoremove             # Remove unused dependencies
```

**Common workflow:**
```bash
sudo apt update                 # Update package lists
sudo apt upgrade                # Upgrade installed packages
sudo apt autoremove             # Remove unused dependencies
```

---

### dpkg (Debian Package Manager)

Low-level tool for managing .deb packages.

**Install a .deb package:**
```bash
sudo dpkg -i package.deb
```

**Remove a package:**
```bash
sudo dpkg -r package-name
```

**List installed packages:**
```bash
dpkg -l
```

**List packages matching pattern:**
```bash
dpkg -l | grep search-term
```

**Show package information:**
```bash
dpkg -s package-name
```

**Show package contents:**
```bash
dpkg -L package-name            # List files installed by package
```

**Find which package owns a file:**
```bash
dpkg -S /path/to/file
```

**Check package installation status:**
```bash
dpkg -l | grep package-name
```

**Force install with dependencies:**
```bash
sudo apt install -f
```

**Common dpkg options:**
```bash
dpkg -i         # Install
dpkg -r         # Remove (keep configuration)
dpkg -P         # Purge (remove with configuration)
dpkg -l         # List packages
dpkg -s         # Show status
dpkg -L         # List files
dpkg -S         # Search file
```

---

### Package Management Workflow

**Install software:**
```bash
sudo apt update
sudo apt install git
```

**Update system:**
```bash
sudo apt update
sudo apt upgrade
```

**Remove unused packages:**
```bash
sudo apt autoremove
sudo apt autoclean
```

**Check for installed package:**
```bash
apt list --installed | grep package-name
```

**Install from .deb file:**
```bash
sudo dpkg -i downloaded-package.deb
sudo apt install -f              # Fix any broken dependencies
```

---

## Networking Commands

### ifconfig (Interface Configuration)

Displays network interface configuration (legacy command, often replaced by `ip`).

**Show all network interfaces:**
```bash
ifconfig
```

**Show specific interface:**
```bash
ifconfig eth0
```

**Enable network interface:**
```bash
sudo ifconfig eth0 up
```

**Disable network interface:**
```bash
sudo ifconfig eth0 down
```

**Set IP address:**
```bash
sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0
```

**Output explanation:**
```
eth0: flags=UP,BROADCAST,RUNNING,MULTICAST  mtu 1500
    inet 192.168.1.100  netmask 255.255.255.0  broadcast 192.168.1.255
    inet6 fe80::1  prefixlen 64  scopeid 0x20<link>
    ether 00:11:22:33:44:55  txqueuelen 1000  (Ethernet)
    RX packets 12345  bytes 9876543 (9.4 MiB)
    RX errors 0  dropped 0  overruns 0  frame 0
    TX packets 54321  bytes 3456789 (3.2 MiB)
    TX errors 0  dropped 0  overruns 0  carrier 0  collisions 0
```

**Modern alternative (ip command):**
```bash
ip addr show                    # Show all interfaces
ip addr show eth0               # Show specific interface
ip link set eth0 up             # Enable interface
ip link set eth0 down           # Disable interface
ip addr add 192.168.1.100/24 dev eth0   # Add IP address
```

---

### ping (Packet Internet Groper)

Tests connectivity to a remote host.

**Ping a host:**
```bash
ping google.com
```

**Ping with specific number of requests:**
```bash
ping -c 4 google.com            # Linux/Mac
ping -n 4 google.com            # Windows
```

**Ping with timeout:**
```bash
ping -w 10000 google.com        # Timeout after 10 seconds
```

**Ping with specific packet size:**
```bash
ping -s 1000 google.com
```

**Ping IP address:**
```bash
ping 8.8.8.8
```

**Ping with verbose output:**
```bash
ping -v google.com
```

**Output explanation:**
```
PING google.com (142.250.80.46) 56(84) bytes of data.
64 bytes from google.com (142.250.80.46): icmp_seq=1 ttl=115 time=23.4 ms
64 bytes from google.com (142.250.80.46): icmp_seq=2 ttl=115 time=22.1 ms
64 bytes from google.com (142.250.80.46): icmp_seq=3 ttl=115 time=21.9 ms
64 bytes from google.com (142.250.80.46): icmp_seq=4 ttl=115 time=22.3 ms

--- google.com statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/stddev = 21.9/22.4/23.4/0.6 ms
```

---

### netstat (Network Statistics)

Displays network connections, routing tables, and interface statistics.

**Show all connections:**
```bash
netstat -a
```

**Show listening ports:**
```bash
netstat -l
```

**Show listening TCP ports:**
```bash
netstat -lt
```

**Show listening UDP ports:**
```bash
netstat -lu
```

**Show established connections:**
```bash
netstat -t
```

**Show connection with process ID:**
```bash
sudo netstat -tlnp
```

**Show routing table:**
```bash
netstat -r
```

**Show network interface statistics:**
```bash
netstat -i
```

**Show statistics by protocol:**
```bash
netstat -s
```

**Monitor connections continuously:**
```bash
netstat -c
```

**Output explanation:**
```
Proto Recv-Q Send-Q Local Address       Foreign Address    State
tcp   0      0      127.0.0.1:22        0.0.0.0:*          LISTEN
tcp   0      0      192.168.1.100:443   10.0.0.50:54321   ESTABLISHED
udp   0      0      0.0.0.0:53          0.0.0.0:*
```

**Modern alternative (ss command):**
```bash
ss -tlnp                        # Show listening ports with process info
ss -at                          # Show all TCP connections
ss -au                          # Show all UDP connections
ss -s                           # Show statistics
```

**Common options:**
```bash
netstat -tlnp    # TCP, Listening, Numeric, Process info
netstat -ulnp    # UDP, Listening, Numeric, Process info
netstat -tlnpe   # TCP, Listening, Numeric, Process, Extended
```

---

### traceroute (Trace Route)

Shows the path taken by packets to reach a destination host.

**Basic traceroute:**
```bash
traceroute google.com
```

**Traceroute to IP address:**
```bash
traceroute 8.8.8.8
```

**Limit number of hops:**
```bash
traceroute -m 10 google.com
```

**Use specific port:**
```bash
traceroute -p 80 google.com
```

**Set timeout for each probe:**
```bash
traceroute -w 5 google.com
```

**Verbose output:**
```bash
traceroute -v google.com
```

**Output explanation:**
```
traceroute to google.com (142.250.80.46), 30 hops max, 60 byte packets
 1  router.local (192.168.1.1)  1.234 ms  1.123 ms  1.456 ms
 2  isp-gateway (10.0.0.1)  5.678 ms  5.234 ms  5.891 ms
 3  core-router.isp (203.0.113.1)  12.345 ms  12.789 ms  11.234 ms
 4  google-gw.net (142.250.1.1)  18.901 ms  18.456 ms  19.234 ms
 5  google.com (142.250.80.46)  20.123 ms  19.789 ms  20.456 ms
```

**Modern alternative (mtr - My Traceroute):**
```bash
mtr google.com                  # Real-time traceroute with statistics
mtr -c 10 google.com            # Send 10 cycles
mtr -r google.com               # Report mode (single output)
```

**On Windows:**
```bash
tracert google.com
```

---

### Additional Useful Networking Commands

**Get hostname:**
```bash
hostname
```

**Get FQDN (Fully Qualified Domain Name):**
```bash
hostname -f
```

**Get IP address:**
```bash
hostname -I                     # Show all IP addresses
```

**DNS lookup (nslookup):**
```bash
nslookup google.com
nslookup 8.8.8.8                # Reverse DNS lookup
```

**DNS query (dig):**
```bash
dig google.com                  # Full DNS query
dig google.com +short           # Short output
dig @8.8.8.8 google.com         # Query specific DNS server
```

**Show routing table:**
```bash
route -n                        # Numeric output
ip route show                   # Modern alternative
```

**Test port connectivity:**
```bash
telnet hostname port
nc -zv hostname port            # netcat
curl http://hostname:port       # HTTP request
```

**Show network interfaces:**
```bash
ip link show                    # Modern command
ifconfig                        # Legacy command
```

**Get MAC address:**
```bash
ifconfig | grep HWaddr
ip link show                    # Shows MAC addresses
```

---

## Quick Reference Table

| Command | Purpose | Example |
|---------|---------|---------|
| `pwd` | Print working directory | `pwd` |
| `ls` | List files | `ls -la` |
| `cd` | Change directory | `cd /home/user` |
| `chmod` | Change permissions | `chmod 755 file.sh` |
| `chown` | Change ownership | `sudo chown user:group file` |
| `apt update` | Update package lists | `sudo apt update` |
| `apt install` | Install package | `sudo apt install git` |
| `dpkg -i` | Install .deb file | `sudo dpkg -i package.deb` |
| `ifconfig` | Show network interfaces | `ifconfig` |
| `ping` | Test connectivity | `ping google.com` |
| `netstat` | Network statistics | `sudo netstat -tlnp` |
| `traceroute` | Show route to host | `traceroute google.com` |

---

## Common Workflows

### Setting up a new project directory

```bash
mkdir myproject
cd myproject
chmod 755 myproject
ls -la
```

### Installing and managing software

```bash
sudo apt update
sudo apt install software-name
apt show software-name
which software-name
```

### Checking network connectivity

```bash
ping 8.8.8.8
traceroute google.com
netstat -tlnp
ifconfig
```

### Managing file permissions

```bash
chmod u+x script.sh             # Make executable
chmod 644 document.txt          # Read-write for owner, read for others
sudo chown user:group file.txt  # Change ownership
ls -l file.txt                  # Verify permissions
```

---

**Note:** Some commands require sudo (superuser do) privileges. Always be careful when using chmod, chown, and package management commands with sudo.