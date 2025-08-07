# Complete Linux Commands Reference

## Table of Contents

1. [User Information](#user-information)
2. [File and Directory Commands](#file-and-directory-commands)
3. [File Permissions](#file-permissions)
4. [Text Processing](#text-processing)
5. [System and Hardware Information](#system-and-hardware-information)
6. [Process Management](#process-management)
7. [Networking](#networking)
8. [Package Management](#package-management)
9. [Disk Usage](#disk-usage)
10. [Search Commands](#search-commands)
11. [SSH Commands](#ssh-commands)
12. [Vi/Vim Commands](#vivim-commands)
13. [Archive and Compression](#archive-and-compression)
14. [System Control](#system-control)
15. [Environment Variables](#environment-variables)
16. [Cron Jobs](#cron-jobs)
17. [Performance Monitoring](#performance-monitoring)

---

## User Information

### who
Display information about currently logged-in users
```bash
# Basic usage
who

# Show all information including boot time, runlevel
who -a

# Show only usernames
who -q

# Output example
# john     pts/0        2025-01-08 10:30 (192.168.1.10)
```

### whoami
Display current username
```bash
whoami
# Output: john
```

### id
Display user and group IDs
```bash
# Show current user's ID
id

# Show specific user's ID
id username

# Show only user ID
id -u

# Show only group ID
id -g

# Output example
# uid=1000(john) gid=1000(john) groups=1000(john),4(adm),27(sudo)
```

### groups
Display all groups for current user
```bash
# Show groups for current user
groups

# Show groups for specific user
groups username

# Output example
# john : john adm cdrom sudo dip plugdev lpadmin
```

### users
Display usernames of all logged-in users
```bash
users
# Output: john mary admin
```

### finger
Display detailed user information
```bash
# Show info for all users
finger

# Show info for specific user
finger username

# Note: May need installation
sudo apt install finger
```

### w
Display who is logged on and what they are doing
```bash
# Show all users and their activities
w

# Show specific user
w username

# Don't show header
w -h

# Output example
# 10:30:04 up 2:09, 1 user, load average: 0.09, 0.07, 0.02
# USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT
# john :0 :0 08:27 ?xdm? 1:14 0.01s /usr/lib/gdm3/g
```

### last
Show last logins
```bash
# Show last logins
last

# Show specific user's logins
last username

# Show last N entries
last -n 10

# Show logins since specific date
last -s yesterday
```

### lastlog
Show most recent login of all users
```bash
# Show all users
lastlog

# Show specific user
lastlog -u username

# Show logins from last N days
lastlog -t 7
```

---

## File and Directory Commands

### pwd
Print current working directory
```bash
pwd
# Output: /home/john/Documents
```

### ls
List directory contents
```bash
# Basic listing
ls

# Long format with details
ls -l

# Show hidden files
ls -a

# Human readable file sizes
ls -lh

# Sort by modification time
ls -lt

# Sort by size
ls -lS

# Recursive listing
ls -R

# One file per line
ls -1

# Color output
ls --color=auto

# List specific directory
ls /path/to/directory

# Combined options
ls -lah
```

### cd
Change directory
```bash
# Go to home directory
cd
cd ~

# Go to specific directory
cd /path/to/directory

# Go to parent directory
cd ..

# Go to previous directory
cd -

# Go up two levels
cd ../../

# Go to root directory
cd /
```

### mkdir
Create directories
```bash
# Create single directory
mkdir directory_name

# Create multiple directories
mkdir dir1 dir2 dir3

# Create nested directories
mkdir -p parent/child/grandchild

# Set permissions while creating
mkdir -m 755 directory_name

# Verbose output
mkdir -v directory_name
```

### rmdir
Remove empty directories
```bash
# Remove empty directory
rmdir directory_name

# Remove multiple empty directories
rmdir dir1 dir2 dir3

# Remove parent directories if empty
rmdir -p parent/child/grandchild

# Ignore non-empty directories
rmdir --ignore-fail-on-non-empty directory_name
```

### rm
Remove files and directories
```bash
# Remove file
rm filename

# Remove multiple files
rm file1 file2 file3

# Remove with confirmation
rm -i filename

# Force remove without confirmation
rm -f filename

# Remove directory recursively
rm -r directory_name

# Force remove directory recursively
rm -rf directory_name

# Remove files matching pattern
rm *.txt

# Verbose output
rm -v filename
```

### cp
Copy files and directories
```bash
# Copy file
cp source destination

# Copy multiple files to directory
cp file1 file2 file3 destination_directory/

# Copy directory recursively
cp -r source_directory destination_directory

# Preserve file attributes
cp -p source destination

# Interactive mode (confirm overwrites)
cp -i source destination

# Update (copy only if source is newer)
cp -u source destination

# Verbose output
cp -v source destination

# Create backup of destination
cp --backup source destination
```

### mv
Move/rename files and directories
```bash
# Rename file
mv oldname newname

# Move file to directory
mv file directory/

# Move multiple files
mv file1 file2 file3 directory/

# Move with confirmation
mv -i source destination

# Update only if source is newer
mv -u source destination

# Verbose output
mv -v source destination

# Create backup of destination
mv --backup source destination
```

### touch
Create empty files or update timestamps
```bash
# Create new empty file
touch filename

# Create multiple files
touch file1 file2 file3

# Update access time only
touch -a filename

# Update modification time only
touch -m filename

# Set specific timestamp
touch -t 202501081030 filename

# Use another file's timestamp
touch -r reference_file target_file

# Don't create file if it doesn't exist
touch -c filename
```

### ln
Create links between files
```bash
# Create hard link
ln source_file link_name

# Create symbolic link
ln -s source_file link_name

# Create symbolic link to directory
ln -s /path/to/directory link_name

# Force creation (overwrite existing)
ln -sf source_file link_name

# Verbose output
ln -sv source_file link_name
```

---

## File Permissions

### chmod
Change file permissions
```bash
# Numeric method (octal)
chmod 755 filename      # rwxr-xr-x
chmod 644 filename      # rw-r--r--
chmod 600 filename      # rw-------
chmod 777 filename      # rwxrwxrwx

# Symbolic method
chmod u+x filename      # Add execute for user
chmod g-w filename      # Remove write for group
chmod o+r filename      # Add read for others
chmod a+x filename      # Add execute for all

# Multiple changes
chmod u+rw,g+r,o-rwx filename

# Recursive changes
chmod -R 755 directory/

# Reference another file's permissions
chmod --reference=ref_file target_file

# Permission meanings:
# r = 4 (read)
# w = 2 (write)  
# x = 1 (execute)
# - = 0 (no permission)
```

### chown
Change file ownership
```bash
# Change owner only
chown username filename

# Change owner and group
chown username:groupname filename
chown username.groupname filename

# Change group only
chown :groupname filename

# Recursive changes
chown -R username:groupname directory/

# Use numeric IDs
chown 1000:1000 filename

# Reference another file's ownership
chown --reference=ref_file target_file
```

### chgrp
Change group ownership
```bash
# Change group
chgrp groupname filename

# Recursive changes
chgrp -R groupname directory/

# Reference another file's group
chgrp --reference=ref_file target_file

# Use numeric group ID
chgrp 1000 filename
```

### umask
Set default file permissions
```bash
# Show current umask
umask

# Set umask (files will be created with 644, directories with 755)
umask 022

# Set umask with symbolic notation
umask u=rwx,g=rx,o=rx
```

---

## Text Processing

### cat
Display file contents
```bash
# Display file
cat filename

# Display multiple files
cat file1 file2

# Create new file
cat > newfile.txt
# Type content, then Ctrl+D to save

# Append to file
cat >> filename

# Number lines
cat -n filename

# Show line endings
cat -E filename

# Show tabs as ^I
cat -T filename

# Show all non-printing characters
cat -A filename

# Squeeze multiple blank lines
cat -s filename
```

### less
View file contents page by page
```bash
# View file
less filename

# Search forward
/search_term

# Search backward
?search_term

# Go to next occurrence
n

# Go to previous occurrence
N

# Go to beginning
g

# Go to end
G

# Quit
q

# View multiple files
less file1 file2
```

### more
View file contents page by page (basic)
```bash
# View file
more filename

# Space = next page
# Enter = next line
# q = quit
# b = previous page
```

### head
Display first lines of file
```bash
# Show first 10 lines (default)
head filename

# Show first N lines
head -n 20 filename
head -20 filename

# Show first N bytes
head -c 100 filename

# Show multiple files
head file1 file2

# Follow file (like tail -f)
head -f filename
```

### tail
Display last lines of file
```bash
# Show last 10 lines (default)
tail filename

# Show last N lines
tail -n 20 filename
tail -20 filename

# Show last N bytes
tail -c 100 filename

# Follow file (monitor for changes)
tail -f filename

# Follow multiple files
tail -f file1 file2

# Start from line N
tail -n +10 filename
```

### grep
Search text patterns
```bash
# Basic search
grep "pattern" filename

# Case-insensitive search
grep -i "pattern" filename

# Search recursively
grep -r "pattern" directory/

# Show line numbers
grep -n "pattern" filename

# Show only matching part
grep -o "pattern" filename

# Invert match (show non-matching lines)
grep -v "pattern" filename

# Count matches
grep -c "pattern" filename

# Multiple patterns
grep -E "pattern1|pattern2" filename

# Whole word match
grep -w "word" filename

# Search multiple files
grep "pattern" file1 file2

# Regular expressions
grep "^start" filename        # Lines starting with "start"
grep "end$" filename          # Lines ending with "end"
grep "..." filename           # Lines with exactly 3 characters
```

### sed
Stream editor for text manipulation
```bash
# Replace first occurrence
sed 's/old/new/' filename

# Replace all occurrences
sed 's/old/new/g' filename

# Replace and save to file
sed 's/old/new/g' filename > newfile

# In-place editing
sed -i 's/old/new/g' filename

# Delete lines containing pattern
sed '/pattern/d' filename

# Delete line N
sed '5d' filename

# Delete lines N to M
sed '5,10d' filename

# Print specific lines
sed -n '5,10p' filename

# Insert line before pattern
sed '/pattern/i\New line' filename

# Append line after pattern
sed '/pattern/a\New line' filename
```

### awk
Text processing tool
```bash
# Print specific column
awk '{print $1}' filename

# Print multiple columns
awk '{print $1, $3}' filename

# Print with custom separator
awk -F: '{print $1}' /etc/passwd

# Print lines matching pattern
awk '/pattern/ {print}' filename

# Sum numbers in column
awk '{sum+=$1} END {print sum}' filename

# Count lines
awk 'END {print NR}' filename

# Print line numbers
awk '{print NR, $0}' filename

# Conditional processing
awk '$3 > 100 {print $1}' filename
```

### sort
Sort lines in text files
```bash
# Basic sort
sort filename

# Reverse sort
sort -r filename

# Numeric sort
sort -n filename

# Sort by specific column
sort -k2 filename

# Sort and remove duplicates
sort -u filename

# Case-insensitive sort
sort -f filename

# Sort by size (human readable)
sort -h filename

# Random sort
sort -R filename

# Merge sorted files
sort -m file1 file2
```

### uniq
Report or omit repeated lines
```bash
# Remove adjacent duplicates
uniq filename

# Count occurrences
uniq -c filename

# Show only duplicates
uniq -d filename

# Show only unique lines
uniq -u filename

# Ignore case
uniq -i filename

# Skip first N fields
uniq -f N filename

# Skip first N characters
uniq -s N filename
```

### wc
Count lines, words, and characters
```bash
# Count lines, words, characters
wc filename

# Count lines only
wc -l filename

# Count words only
wc -w filename

# Count characters only
wc -c filename

# Count bytes
wc -c filename

# Count multiple files
wc file1 file2

# Read from stdin
cat filename | wc -l
```

### cut
Extract columns from text
```bash
# Cut by character position
cut -c1-10 filename

# Cut by field (default delimiter: tab)
cut -f1,3 filename

# Cut by field with custom delimiter
cut -d: -f1 filename

# Cut from character N to end
cut -c5- filename

# Cut everything except specified fields
cut --complement -f2 filename
```

### tr
Translate or delete characters
```bash
# Convert lowercase to uppercase
tr 'a-z' 'A-Z' < filename

# Delete specific characters
tr -d 'aeiou' < filename

# Squeeze repeated characters
tr -s ' ' < filename

# Replace characters
echo "hello world" | tr ' ' '_'

# Delete newlines
tr -d '\n' < filename
```

---

## System and Hardware Information

### uname
System information
```bash
# Show all information
uname -a

# Show kernel name
uname -s

# Show kernel release
uname -r

# Show kernel version
uname -v

# Show machine architecture
uname -m

# Show processor type
uname -p

# Show hardware platform
uname -i

# Show operating system
uname -o
```

### lscpu
Display CPU information
```bash
# Show CPU details
lscpu

# Show CPU in parseable format
lscpu -p
```

### lsblk
List block devices
```bash
# List all block devices
lsblk

# Show filesystem information
lsblk -f

# Show device permissions
lsblk -m

# Show specific device
lsblk /dev/sda
```

### lsusb
List USB devices
```bash
# List all USB devices
lsusb

# Verbose output
lsusb -v

# Show device tree
lsusb -t
```

### lspci
List PCI devices
```bash
# List all PCI devices
lspci

# Verbose output
lspci -v

# Very verbose output
lspci -vv

# Show numeric IDs
lspci -n
```

### free
Display memory usage
```bash
# Show memory usage
free

# Human readable format
free -h

# Show in megabytes
free -m

# Show in gigabytes
free -g

# Continuous monitoring
free -s 5
```

### df
Display filesystem disk usage
```bash
# Show all filesystems
df

# Human readable format
df -h

# Show inodes usage
df -i

# Show filesystem type
df -T

# Show specific filesystem
df /home
```

### lsof
List open files
```bash
# List all open files
lsof

# List files opened by specific user
lsof -u username

# List files opened by specific process
lsof -p PID

# List files for specific port
lsof -i :80

# List network connections
lsof -i

# List files in specific directory
lsof +D /path/to/directory
```

### dmidecode
Display hardware information
```bash
# Show all hardware info (requires root)
sudo dmidecode

# Show specific type
sudo dmidecode -t memory
sudo dmidecode -t processor
sudo dmidecode -t system

# Quiet output
sudo dmidecode -q
```

---

## Process Management

### ps
Display running processes
```bash
# Show processes for current user
ps

# Show all processes
ps aux

# Show processes in tree format
ps -ef --forest

# Show specific user's processes
ps -u username

# Show processes by name
ps -C process_name

# Custom format
ps -eo pid,ppid,cmd,%mem,%cpu

# Real-time updates
ps aux --sort=-%cpu
```

### top
Display real-time process information
```bash
# Basic usage
top

# Sort by CPU usage
top -o %CPU

# Sort by memory usage
top -o %MEM

# Show specific user's processes
top -u username

# Batch mode (non-interactive)
top -b

# Show specific number of processes
top -n 1

# Update interval in seconds
top -d 5
```

### htop
Enhanced version of top
```bash
# Basic usage (if installed)
htop

# Show specific user
htop -u username

# Show process tree
htop -t
```

### jobs
Display active jobs
```bash
# Show current jobs
jobs

# Show with process IDs
jobs -l

# Show only running jobs
jobs -r

# Show only stopped jobs
jobs -s
```

### bg
Put jobs in background
```bash
# Put current job in background
bg

# Put specific job in background
bg %1
```

### fg
Bring jobs to foreground
```bash
# Bring most recent job to foreground
fg

# Bring specific job to foreground
fg %1
```

### nohup
Run command immune to hangups
```bash
# Run command in background
nohup command &

# Redirect output
nohup command > output.log 2>&1 &
```

### kill
Terminate processes
```bash
# Kill process by PID
kill 1234

# Force kill
kill -9 1234

# Kill by name (all instances)
killall process_name

# Kill with specific signal
kill -TERM 1234

# List available signals
kill -l

# Kill all processes by user
pkill -u username

# Kill processes matching pattern
pkill -f pattern
```

### killall
Kill processes by name
```bash
# Kill all instances of a process
killall process_name

# Force kill
killall -9 process_name

# Interactive mode
killall -i process_name

# Kill processes by user
killall -u username process_name
```

### pgrep
Find process IDs by name
```bash
# Find PIDs by name
pgrep process_name

# Find with full command line
pgrep -f pattern

# Find by user
pgrep -u username

# Find newest process
pgrep -n process_name

# Find oldest process
pgrep -o process_name
```

---

## Networking

### ping
Test network connectivity
```bash
# Basic ping
ping hostname

# Ping specific number of times
ping -c 4 hostname

# Set packet size
ping -s 1024 hostname

# Quiet output (summary only)
ping -q hostname

# Flood ping (root only)
ping -f hostname

# Set timeout
ping -W 2 hostname
```

### wget
Download files from web
```bash
# Download file
wget URL

# Download to specific directory
wget -P /path/to/directory URL

# Download with different filename
wget -O filename URL

# Continue partial download
wget -c URL

# Download recursively
wget -r URL

# Background download
wget -b URL

# Set user agent
wget --user-agent="Custom Agent" URL

# Download with authentication
wget --user=username --password=password URL
```

### curl
Transfer data from/to servers
```bash
# Basic GET request
curl URL

# Save to file
curl -o filename URL

# Follow redirects
curl -L URL

# Include headers in output
curl -i URL

# POST request with data
curl -X POST -d "data" URL

# Upload file
curl -X POST -F "file=@filename" URL

# Set headers
curl -H "Content-Type: application/json" URL

# Basic authentication
curl -u username:password URL

# Silent mode
curl -s URL

# Verbose output
curl -v URL
```

### netstat
Display network connections
```bash
# Show all connections
netstat -a

# Show listening ports
netstat -l

# Show TCP connections
netstat -t

# Show UDP connections
netstat -u

# Show process names
netstat -p

# Show numerical addresses
netstat -n

# Show routing table
netstat -r

# Continuous monitoring
netstat -c
```

### ss
Socket statistics (replacement for netstat)
```bash
# Show all sockets
ss -a

# Show listening sockets
ss -l

# Show TCP sockets
ss -t

# Show UDP sockets
ss -u

# Show process names
ss -p

# Show numerical addresses
ss -n

# Show specific port
ss -ltn sport = :80
```

### ifconfig
Configure network interfaces
```bash
# Show all interfaces
ifconfig

# Show specific interface
ifconfig eth0

# Bring interface up
ifconfig eth0 up

# Bring interface down
ifconfig eth0 down

# Set IP address
ifconfig eth0 192.168.1.100

# Set netmask
ifconfig eth0 192.168.1.100 netmask 255.255.255.0
```

### ip
Advanced network configuration
```bash
# Show all interfaces
ip addr show

# Show routing table
ip route show

# Add IP address
ip addr add 192.168.1.100/24 dev eth0

# Delete IP address
ip addr del 192.168.1.100/24 dev eth0

# Bring interface up
ip link set eth0 up

# Bring interface down
ip link set eth0 down

# Add route
ip route add 192.168.1.0/24 via 192.168.1.1

# Delete route
ip route del 192.168.1.0/24
```

### iptables
Firewall configuration
```bash
# List rules
iptables -L

# List with line numbers
iptables -L --line-numbers

# Allow incoming SSH
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Block specific IP
iptables -A INPUT -s 192.168.1.100 -j DROP

# Delete rule
iptables -D INPUT 1

# Flush all rules
iptables -F

# Save rules (depends on distribution)
iptables-save > /etc/iptables/rules.v4
```

### nmap
Network exploration and security auditing
```bash
# Scan single host
nmap hostname

# Scan IP range
nmap 192.168.1.1-254

# Scan specific ports
nmap -p 22,80,443 hostname

# TCP SYN scan
nmap -sS hostname

# UDP scan
nmap -sU hostname

# OS detection
nmap -O hostname

# Service version detection
nmap -sV hostname

# Aggressive scan
nmap -A hostname
```

---

## Package Management

### APT (Debian/Ubuntu)

```bash
# Update package list
apt update

# Upgrade packages
apt upgrade

# Full upgrade
apt full-upgrade

# Install package
apt install package_name

# Remove package
apt remove package_name

# Remove package and config files
apt purge package_name

# Search packages
apt search keyword

# Show package information
apt show package_name

# List installed packages
apt list --installed

# Clean package cache
apt clean

# Remove unnecessary packages
apt autoremove
```

### YUM (Red Hat/CentOS)

```bash
# Update package list
yum update

# Install package
yum install package_name

# Remove package
yum remove package_name

# Search packages
yum search keyword

# Show package information
yum info package_name

# List installed packages
yum list installed

# Clean cache
yum clean all

# Show package dependencies
yum deplist package_name
```

### DNF (Fedora)

```bash
# Update packages
dnf update

# Install package
dnf install package_name

# Remove package
dnf remove package_name

# Search packages
dnf search keyword

# Show package information
dnf info package_name

# List installed packages
dnf list installed

# Clean cache
dnf clean all
```

### RPM (Red Hat Package Manager)

```bash
# Install RPM package
rpm -i package.rpm

# Upgrade package
rpm -U package.rpm

# Remove package
rpm -e package_name

# Query installed packages
rpm -qa

# Query package information
rpm -qi package_name

# List files in package
rpm -ql package_name

# Find which package owns a file
rpm -qf /path/to/file
```

### Snap

```bash
# Install snap package
snap install package_name

# List installed snaps
snap list

# Update all snaps
snap refresh

# Remove snap
snap remove package_name

# Search snaps
snap find keyword

# Show snap information
snap info package_name
```

---

## Disk Usage

### du
Display directory space usage
```bash
# Show directory sizes
du

# Human readable format
du -h

# Summary only (total)
du -s

# Show sizes for all files
du -a

# Maximum depth
du --max-depth=2

# Exclude specific files
du --exclude="*.log"

# Sort by size
du -h | sort -rh

# Show largest directories
du -h --max-depth=1 | sort -rh
```

### df
Display filesystem space usage
```bash
# Show filesystem usage
df

# Human readable format
df -h

# Show inode usage
df -i

# Show filesystem types
df -T

# Show only specific filesystem type
df -t ext4
```

### fdisk
Manage disk partitions
```bash
# List all disks
fdisk -l

# Interactive mode for specific disk
fdisk /dev/sda

# Show specific disk
fdisk -l /dev/sda
```

### mount
Mount filesystems
```bash
# Show all mounted filesystems
mount

# Mount filesystem
mount /dev/sda1 /mnt/mydisk

# Mount with specific filesystem type
mount -t ext4 /dev/sda1 /mnt/mydisk

# Mount read-only
mount -o ro /dev/sda1 /mnt/mydisk

# Mount with specific options
mount -o noexec,nosuid /dev/sda1 /mnt/mydisk

# Bind mount
mount --bind /source /destination
```

### umount
Unmount filesystems
```bash
# Unmount by mount point
umount /mnt/mydisk

# Unmount by device
umount /dev/sda1

# Force unmount
umount -f /mnt/mydisk

# Lazy unmount
umount -l /mnt/mydisk

# Show what's preventing unmount
lsof /mnt/mydisk
```

---

## Search Commands

### find
Search for files and directories
```bash
# Find by name
find /path -name "filename"

# Case-insensitive search
find /path -iname "filename"

# Find by type
find /path -type f    # files only
find /path -type d    # directories only

# Find by size
find /path -size +100M    # larger than 100MB
find /path -size -1M      # smaller than 1MB

# Find by modification time
find /path -mtime -7      # modified in last 7 days
find /path -mtime +30     # modified more than 30 days ago

# Find by permissions
find /path -perm 644

# Find and execute command
find /path -name "*.tmp" -exec rm {} \;

# Find empty files/directories
find /path -empty

# Find by owner
find /path -user username

# Find by group
find /path -group groupname

# Multiple conditions
find /path -name "*.txt" -size +1M -mtime -7
```

### locate
Find files quickly using database
```bash
# Find files by name
locate filename

# Case-insensitive search
locate -i filename

# Limit number of results
locate -n 10 filename

# Update database
updatedb

# Show statistics
locate -S
```

### whereis
Locate binary, source, and manual files
```bash
# Find binary, source, and manual
whereis command

# Binary files only
whereis -b command

# Manual pages only
whereis -m command

# Source files only
whereis -s command
```

### which
Locate a command
```bash
# Find command location
which command

# Show all locations
which -a command
```

### apropos
Search manual pages
```bash
# Search for keyword in manual pages
apropos keyword

# Search in descriptions only
apropos -s 1 keyword
```

---

## SSH Commands

### ssh
Secure Shell client
```bash
# Connect to server
ssh username@hostname

# Connect using specific port
ssh -p 2222 username@hostname

# Connect with specific private key
ssh -i ~/.ssh/private_key username@hostname

# Execute command remotely
ssh username@hostname 'ls -la'

# Enable X11 forwarding
ssh -X username@hostname

# Create tunnel (port forwarding)
ssh -L 8080:localhost:80 username@hostname

# Background connection
ssh -f username@hostname

# Verbose output
ssh -v username@hostname
```

### ssh-keygen
Generate SSH keys
```bash
# Generate RSA key pair
ssh-keygen -t rsa

# Generate with specific key size
ssh-keygen -t rsa -b 4096

# Generate with comment
ssh-keygen -t rsa -C "your_email@example.com"

# Generate Ed25519 key
ssh-keygen -t ed25519

# Generate without passphrase
ssh-keygen -t rsa -N ""

# Change key passphrase
ssh-keygen -p -f ~/.ssh/id_rsa
```

### ssh-copy-id
Copy SSH keys to remote server
```bash
# Copy public key to server
ssh-copy-id username@hostname

# Copy specific key
ssh-copy-id -i ~/.ssh/id_rsa.pub username@hostname

# Use specific port
ssh-copy-id -p 2222 username@hostname
```

### scp
Secure copy over SSH
```bash
# Copy file to remote server
scp localfile username@hostname:/remote/path/

# Copy file from remote server
scp username@hostname:/remote/file /local/path/

# Copy directory recursively
scp -r directory/ username@hostname:/remote/path/

# Use specific port
scp -P 2222 file username@hostname:/path/

# Preserve file attributes
scp -p file username@hostname:/path/

# Verbose output
scp -v file username@hostname:/path/
```

### rsync
Efficient file synchronization
```bash
# Sync directories
rsync -av source/ destination/

# Sync to remote server
rsync -av source/ username@hostname:/path/

# Sync with progress
rsync -av --progress source/ destination/

# Exclude files
rsync -av --exclude="*.log" source/ destination/

# Delete files not in source
rsync -av --delete source/ destination/

# Dry run (preview changes)
rsync -av --dry-run source/ destination/

# Compress during transfer
rsync -avz source/ username@hostname:/path/
```

---

## Vi/Vim Commands

### Basic Vim Usage

```bash
# Open file
vi filename
vim filename

# Create new file
vi newfile.txt

# Open at specific line
vim +10 filename

# Open multiple files
vim file1 file2 file3

# Open in read-only mode
vim -R filename
```

### Vim Modes

**Command Mode** (default mode)
- Navigate and manipulate text
- Press Esc to enter this mode

**Insert Mode** 
- Type and edit text
- Press i, I, a, A, o, O to enter

**Visual Mode**
- Select text
- Press v, V, or Ctrl+v to enter

### Navigation Commands

```bash
# Character movement
h          # Move left
j          # Move down  
k          # Move up
l          # Move right

# Word movement
w          # Next word beginning
W          # Next WORD beginning
e          # Next word ending
E          # Next WORD ending
b          # Previous word beginning
B          # Previous WORD beginning

# Line movement
0          # Beginning of line
^          # First non-blank character
$          # End of line
G          # Go to last line
gg         # Go to first line
10G        # Go to line 10

# Screen movement
H          # Top of screen
M          # Middle of screen
L          # Bottom of screen
Ctrl+f     # Page down
Ctrl+b     # Page up
Ctrl+d     # Half page down
Ctrl+u     # Half page up
```

### Editing Commands

```bash
# Insert mode
i          # Insert before cursor
I          # Insert at beginning of line
a          # Append after cursor
A          # Append at end of line
o          # Open line below
O          # Open line above

# Delete commands
x          # Delete character under cursor
X          # Delete character before cursor
dw         # Delete word
dd         # Delete entire line
D          # Delete to end of line
3dd        # Delete 3 lines

# Copy and paste
yy         # Copy (yank) line
3yy        # Copy 3 lines
yw         # Copy word
p          # Paste after cursor
P          # Paste before cursor

# Change commands
cw         # Change word
cc         # Change entire line
C          # Change to end of line
r          # Replace single character
R          # Replace mode

# Undo/Redo
u          # Undo
Ctrl+r     # Redo
.          # Repeat last command
```

### Search and Replace

```bash
# Search
/pattern   # Search forward
?pattern   # Search backward
n          # Next occurrence
N          # Previous occurrence
*          # Search word under cursor forward
#          # Search word under cursor backward

# Replace
:s/old/new/           # Replace first occurrence in line
:s/old/new/g          # Replace all in line
:%s/old/new/g         # Replace all in file
:%s/old/new/gc        # Replace all with confirmation
:10,20s/old/new/g     # Replace in lines 10-20
```

### File Operations

```bash
# Save and quit
:w         # Write (save) file
:w filename # Save as filename
:q         # Quit
:q!        # Quit without saving
:wq        # Write and quit
:wq!       # Force write and quit
ZZ         # Write and quit (if modified)
ZQ         # Quit without saving

# File management
:e filename    # Edit another file
:r filename    # Read file into current buffer
:!command      # Execute shell command
```

### Visual Mode

```bash
# Select text
v          # Character-wise selection
V          # Line-wise selection
Ctrl+v     # Block-wise selection

# Operations on selection
d          # Delete selection
y          # Copy selection
c          # Change selection
>          # Indent selection
<          # Unindent selection
```

---

## Archive and Compression

### tar
Archive files
```bash
# Create archive
tar -cf archive.tar files/

# Create compressed archive (gzip)
tar -czf archive.tar.gz files/

# Create compressed archive (bzip2)
tar -cjf archive.tar.bz2 files/

# Extract archive
tar -xf archive.tar

# Extract compressed archive
tar -xzf archive.tar.gz

# List archive contents
tar -tf archive.tar

# Extract to specific directory
tar -xf archive.tar -C /path/to/directory

# Verbose output
tar -vxf archive.tar

# Add files to existing archive
tar -rf archive.tar newfile

# Update files in archive
tar -uf archive.tar files/
```

### gzip
Compress files
```bash
# Compress file
gzip filename

# Decompress file
gzip -d filename.gz
gunzip filename.gz

# Keep original file
gzip -k filename

# Compress with specific level (1-9)
gzip -9 filename

# View compressed file
zcat filename.gz
zless filename.gz
```

### zip
Create and extract ZIP archives
```bash
# Create ZIP archive
zip archive.zip files/

# Create ZIP recursively
zip -r archive.zip directory/

# Extract ZIP archive
unzip archive.zip

# Extract to specific directory
unzip archive.zip -d /path/to/directory

# List ZIP contents
unzip -l archive.zip

# Test ZIP integrity
unzip -t archive.zip

# Extract specific files
unzip archive.zip file1 file2

# Update ZIP archive
zip -u archive.zip newfile
```

### 7zip
Advanced compression tool
```bash
# Create 7z archive
7z a archive.7z files/

# Extract 7z archive
7z x archive.7z

# List archive contents
7z l archive.7z

# Test archive
7z t archive.7z

# Extract to specific directory
7z x archive.7z -o/path/to/directory

# Create with password
7z a -p archive.7z files/
```

---

## System Control

### systemctl
Control systemd services
```bash
# Start service
systemctl start service_name

# Stop service
systemctl stop service_name

# Restart service
systemctl restart service_name

# Reload service configuration
systemctl reload service_name

# Check service status
systemctl status service_name

# Enable service (start at boot)
systemctl enable service_name

# Disable service
systemctl disable service_name

# List all services
systemctl list-units --type=service

# List failed services
systemctl --failed

# Show service logs
journalctl -u service_name
```

### service
Control system services (SysV)
```bash
# Start service
service service_name start

# Stop service
service service_name stop

# Restart service
service service_name restart

# Check status
service service_name status

# List all services
service --status-all
```

### chkconfig
Configure services (Red Hat/CentOS)
```bash
# List services
chkconfig --list

# Enable service
chkconfig service_name on

# Disable service
chkconfig service_name off

# Check service status
chkconfig service_name
```

### update-rc.d
Configure services (Debian/Ubuntu)
```bash
# Enable service
update-rc.d service_name enable

# Disable service
update-rc.d service_name disable

# Remove service
update-rc.d service_name remove
```

---

## Environment Variables

### export
Set environment variables
```bash
# Set variable for current session
export VARIABLE_NAME=value

# Set PATH variable
export PATH=$PATH:/new/path

# Show all environment variables
export

# Unset variable
unset VARIABLE_NAME

# Set variable temporarily for command
VARIABLE=value command
```

### env
Display environment variables
```bash
# Show all environment variables
env

# Run command with modified environment
env VARIABLE=value command

# Clear environment and run command
env -i command

# Remove variable from environment
env -u VARIABLE command
```

### printenv
Print environment variables
```bash
# Show all variables
printenv

# Show specific variable
printenv PATH

# Show multiple variables
printenv PATH HOME USER
```

### source / .
Execute script in current shell
```bash
# Source script
source script.sh
. script.sh

# Source bashrc
source ~/.bashrc

# Source with different shell
bash script.sh
```

---

## Cron Jobs

### crontab
Schedule tasks
```bash
# Edit user's crontab
crontab -e

# List user's crontab
crontab -l

# Remove user's crontab
crontab -r

# Edit another user's crontab (root only)
crontab -e -u username

# List another user's crontab
crontab -l -u username
```

### Cron Syntax
```bash
# Format: minute hour day month weekday command
# * * * * * command

# Every minute
* * * * * /path/to/script

# Every hour at minute 0
0 * * * * /path/to/script

# Every day at 2:30 AM
30 2 * * * /path/to/script

# Every Sunday at midnight
0 0 * * 0 /path/to/script

# Every 15 minutes
*/15 * * * * /path/to/script

# Every 2 hours
0 */2 * * * /path/to/script

# Monday to Friday at 9 AM
0 9 * * 1-5 /path/to/script

# First day of every month
0 0 1 * * /path/to/script
```

---

## Performance Monitoring

### iostat
I/O statistics
```bash
# Basic I/O stats
iostat

# Update every 2 seconds
iostat 2

# Show extended statistics
iostat -x

# Show specific device
iostat -x sda

# Show CPU stats only
iostat -c

# Human readable
iostat -h
```

### vmstat
Virtual memory statistics
```bash
# Basic stats
vmstat

# Update every 2 seconds, 5 times
vmstat 2 5

# Show memory in MB
vmstat -S M

# Show disk statistics
vmstat -d

# Show partition statistics
vmstat -p sda1
```

### sar
System activity reporter
```bash
# CPU usage every 2 seconds, 5 times
sar 2 5

# Memory usage
sar -r

# I/O statistics
sar -b

# Network statistics
sar -n DEV

# Load average
sar -q

# Show data from specific date
sar -f /var/log/sa/sa01
```

### uptime
System uptime and load
```bash
# Show uptime and load average
uptime

# Pretty format
uptime -p

# Show since when system is up
uptime -s
```

### dstat
Versatile resource statistics
```bash
# Basic stats
dstat

# CPU stats only
dstat -c

# Memory stats only
dstat -m

# Disk stats only
dstat -d

# Network stats only
dstat -n

# All stats
dstat -a

# Update interval
dstat 5
```

### History Command
Display command history
```bash
# Show command history
history

# Show last N commands
history 10

# Clear history
history -c

# Delete specific entry
history -d 100

# Execute command by number
!100

# Execute last command
!!

# Execute last command with specific text
!grep

# Search history
Ctrl+r

# Show history with timestamps
export HISTTIMEFORMAT="%F %T "
```

### Advanced System Commands

### ldd
Show shared library dependencies
```bash
# Show dependencies
ldd /bin/ls

# Show unused dependencies
ldd -u program

# Show all dependencies
ldd -v program
```

### strace
Trace system calls
```bash
# Trace program execution
strace command

# Trace specific system calls
strace -e open command

# Trace running process
strace -p PID

# Output to file
strace -o output.txt command

# Show timestamps
strace -t command
```

### ltrace
Trace library calls
```bash
# Trace library calls
ltrace command

# Trace specific functions
ltrace -e malloc command

# Trace running process
ltrace -p PID

# Output to file
ltrace -o output.txt command
```

### watch
Execute command repeatedly
```bash
# Run command every 2 seconds
watch command

# Custom interval
watch -n 5 command

# Show differences
watch -d command

# Beep on command failure
watch -b command

# Exit on change
watch -g command
```

### timeout
Run command with time limit
```bash
# Kill command after 30 seconds
timeout 30 command

# Kill with specific signal
timeout --signal=KILL 30 command

# Preserve exit status
timeout --preserve-status 30 command
```

### screen
Terminal multiplexer
```bash
# Start new screen session
screen

# Start with session name
screen -S session_name

# List sessions
screen -ls

# Attach to session
screen -r session_name

# Detach from session (inside screen)
Ctrl+a d

# Kill session
screen -X -S session_name quit
```

### tmux
Terminal multiplexer (modern alternative to screen)
```bash
# Start new session
tmux

# Start with session name
tmux new-session -s session_name

# List sessions
tmux list-sessions

# Attach to session
tmux attach-session -t session_name

# Detach from session (inside tmux)
Ctrl+b d

# Kill session
tmux kill-session -t session_name

# Split window horizontally
Ctrl+b "

# Split window vertically
Ctrl+b %

# Switch between panes
Ctrl+b arrow_key
```

---

## Final Notes

This comprehensive Linux commands reference covers the most commonly used commands across different categories. Each command includes:

- **Basic syntax and usage**
- **Common options and flags**  
- **Practical examples**
- **Related commands for context**

### Tips for Learning:
1. Start with basic file operations (ls, cd, cp, mv)
2. Practice text processing (cat, grep, sed, awk)
3. Learn process management (ps, top, kill)
4. Master file permissions (chmod, chown)
5. Explore networking commands (ping, wget, ssh)

### Additional Resources:
- Use `man command_name` for detailed manual pages
- Use `command_name --help` for quick help
- Use `apropos keyword` to find related commands
- Practice in a safe environment before using on production systems

Remember: Many commands have extensive options. This reference covers the most common use cases, but always check the manual pages for complete documentation.