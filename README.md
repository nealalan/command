# [nealalan.github.io](https://nealalan.github.io)/[command](https://nealalan.github.io/command)

- [iptables essentials](https://nocsma.wordpress.com/2016/10/21/iptables-essentials-common-firewall-rules-and-commands/)

## UPDATES, UPGRADES & PACKAGE MANAGERS

### Mac Package Managers (Darwin)
```bash
# INSTALL APPLE XCODE COMMAND LINE DEV TOOLS
$ xcode-select --install
# INSTALL HOMEBREW / BREW
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# CHECK STATUS OF BREW
$ brew doctor
# INSTALL IFTOP
$ brew install iftop

# SEE WHAT'S INSTALLED
$ brew list && brew cask list
$ system_profiler -detailLevel full SPApplicationsDataType >> installed_software_$(date "+%Y%m%d_%H%M%S").txt
$ brew ls --full-name --versions >>  installed_software_$(date +"%Y%m%d_%H%M%S").txt
# CREATE 'Brewfile' LIST OF INSTALLS & INSTALL LIST IN 'Brewfile'
$ brew bundle dump
$ brew Brewfile
# ... IN UBUNTU
$ sudo apt list --installed >> installed_software_$(date +"%Y%m%d_%H%M%S").txt

# CHECK FOR UPDATES & UPGRADE
$ brew update
$ brew upgrade
```

### Ubuntu Package Manager
```bash
# APT / APT-GET -provides a high-level command line interface for the package management system
#  -y default yes
#  update = d/l package info from all configured sources
#  upgrade = install avai upgrades of all packages 
$ apt update
$ apt upgrade
$ apt install <package>
#  currently installed on the system from the sources configured via sources.list
$ apt-cache search <package>
```

## files
```bash
# DIRECTORY/FILE COLLAPSE
# find all files in this directory and its sub-directories 
# and execute mv with target directory . for each file found 
# to move them to current directory.
# Note: I tried adding mv --backup=numbered but this doesn't work
#  so I added -n to keep from overwriting files with the same name
$ find . -mindepth 2 -type f -print -exec mv -n {} . \;
```
```bash
# ARCHIVE/ZIP 
# -r recursively through dirs
# -dc a nice output
# -9 max compression (no reason not to if storing on the cloud?!)
# can use REGEX with it also :D
$ zip -r -dc -9 archive_name *
```
I use this to sync photos from the source to my iMac
```bash
# SYNC FILES ACROSS COMPUTERS
# --dry-run is obviously removed for the real xfer
$ rsync --dry-run --recursive --compress --progress --delete --itemize-changes ~/Pictures/ neal@192.168.1.42:/Users/Neal/Pictures/All_Photos > ~/Desktop/pic_bkp_$(date +"%Y%m%d_%H%M%S").txt
```
I use this to sync music to backups and other computers
```bash
# SYNCH FILES ACROSS COMPUTER, DISPLAY DELETED FILES ONLY
$ rsync -azP --delete -n ./ /Volumes/USB20FD/Music | grep 'deleting'
```

## git / github / hub

…or create a new repository on the command line
```bash
echo "# neonaluminum.com" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:nealalan/neonaluminum.com.git
git push -u origin master
```
…or push an existing repository from the command line
```bash
git remote add origin git@github.com:nealalan/neonaluminum.com.git
git push -u origin master
```

### git 
```bash
$ git status
$ git push
$ git clone git@github.com:nealalan/command.git
```
a trick i found on stackoverflow when .git/index.lock gives Permission Denied
```bash
$ sudo chown -R : .git  # change group
$ sudo chmod -R 775 .git  # change permission
```

### git setup
```bash
# CREATE SSH KEY TO ADD TO GITHUB
$ ssh-keygen -t rsa -C "neal@email.com"

# TEST OUT THE SSH CONNECTION ON YOUR BOX
$ ssh -T git@github.com

# SET AN HTTPS CLONE TO AN SSH PUSH
# so i pulled down something before I setup ssh and made a bunch of changes 
# i wanted to push back. so I used this command to changed it to SSH push
$ git remote set-url origin git@github.com:nealalan/nealalan.com.git
```

### hub setup
hub is a github utility that lets you *create a repo remotely* 
- [https://hub.github.com/](https://hub.github.com/)
- to use it you'll need to also install [Go](https://medium.com/@patdhlk/how-to-install-go-1-9-1-on-ubuntu-16-04-ee64c073cd79) 

## MONITORING
```bash
# SYSTEM IO MONITORING LOOP
# writes out the activity  on the system every 3 seconts
$ while true ; do iostat -w 3 ; done

# TOP -- display and update sorted information about processes
$ top -o cpu -O +rsize -s 3

# IFTOP -- Interface top in a refreshing screen with cum view
$ sudo iftop -i en0
```
- note-to-self: need to check out mytop, mtop, innotop, mysqladmin

## NETWORKING
```bash
# CURL - Find system settings from the command line
$ curl http://169.254.169.254/

# IFCONFIG - network interface configuration & routing for the computer ports
$ ifconfig en0

# NETSTAT - show network status, network connections, routing tables, interface statistics, masquerade connections, and multicast memberships
#  -r show the routing tables
#  -s Show per-protocol statistics
#  -tu tcp & udp
$ netstat
$ netstat -a | more

# SS
$ ss -l
$ ss -ntp
$ ss -tupl

# NSLOOKUP - QUERY INTERNET NAME SERVERS INTERACTIVELY
# returns the domain name server the IP to domain resolution came from
# -type=SOA : find out the server of authority = might not work
$ nslookup neonaluminum.com
# PING

# DIG - DOMAIN INFORMATION GATHERING
# primarily used for DNS queries of A, TXT, MX, SOA, NS record sets
$ dig neonaluminum.com
# trace trace the domain server of authority (SOA)
$ dig +trace neonaluminum.com
# pull the DNS records (use A, TXT, MX, SOA, NS, ANY)
$ dig neonaluminum.com ANY +noall +answer

# CURL

# WHOIS - QUERY IANA.ORG FOR DOMAIN INFO
$ whois neonaluminum.com

# SHODAN
# DIRB
$ dirb 10.10.50.2
```


### nc / netcat 
TCP & UDP connections and listener
```bash
# NC - PULL A WEBPAGE
$ nc localhost 80
# NC - PORT SCANNING
$ nc -v -w 1 server2.example.com -z 1-1000
# NC - LISTEN FOR A CONNECTION ON PORT 42
#  -v add verbosity
$ nc -v -l 42
# CONNECT TO PORT 42 VIA THE LOOPBACK IP FROM ANOTHER TERM
$ nc -v 127.0.0.1 42
# either side can type and it will echo back
# terminate the connection with ^D (EOF)
```
```bash
# NC - SEND FILES
$ nc -lp 1234 > stuff_to_send.txt
$ nc -w 1 server 1234 < stuff.txt

# LISTEN INTO A FILE
$ nc -v -l 43 > filename.receive
# SEND A FILE TO PORT 43 VIA THE LOOPBACK IP FROM ANOTHER TERM
$ nc -v 127.0.0.1 43 < filename.send
```

### nethogs
```bash
# NETHOGS -- monitor process socket connections 
```

### nmap
nmap can be super noisy and really irritate anyone you run it against recommend you only run it again computers within your internal network or scanme.nmap.org
```bash
# FIND OUT WHAT'S THERE BRUTELY, RECURSIVELY
# this will give you a nice idea of how to hit a server that's poorly configured and open
# -A : enable OS detection and version detection, script scanning and tracert
# -T4 : faster execution (about 1 min for me usually)
# -r : scan ports consecutively
# -p : port range
$ nmap -A -T4 -r -p [1-9999] <address>
#
$ nmap -sC

$ nmap localhost
$ scutil --proxy
$ scutil --dns
$ scutil --get ComputerName
``` 
## METASPLOIT
```bash
# metaspolit console
$ msfconsole
$4search shellshock
$ show options
# LOAD PARMS
$ set RHOST 10.10.50.2
$ set TARGETURI /cgi-bin/test-cgi

```

## SEARCHING
particularly useful when searching for a file or searching for content in a file, such as something suspecious in a log file
```bash
# SEARCH A FILE FOR SPECIFIC CONTENT
# -H : print the filename of each match
# --max-count=#
# -c : suppress output and count matching lines
# -v : inverse matching
# -E : regex pattern search (or text search)
$ cat access.log | grep -E 'php|POST|HEAD|DNS'
```
![](https://raw.githubusercontent.com/nealalan/command/master/grep-E.png)

```bash
# LSOF -- list open files
# huge man file and particularly useful, note security issues with it
$ lsof > ~/open_files.txt
```
## SOCIAL ENGINEERING
```bash
# Discovery
# Harvester

```



## DEV
### maven
apache maven will build your jar files from java source packages. 
```bach
# from your project-dir/pom.xml folder
$ mvn package
# you should end up with BUILD SUCCESSFUL and a folder project-dir/target/
```

### SQL
- sqlmap



## images & graphics
```bash
# ExifTool - Read, Write and Edit Meta Info 
# Info: https://www.sno.phy.queensu.ca/~phil/exiftool/
# Install:
$ brew install exiftool
# Use:
```

## encryption
```bash
# MD5 - calculate a message-digest fingerprint (checksum) for a file
# syntax: md5 [-pqrtx] [-s string] [file ...]
```

## SYSTEM ADMINISTRATION

```bash
ubuntu@nealalan:~$ uname -a
Linux nealalan 4.4.0-1060-aws #69-Ubuntu SMP Sun May 20 13:42:07 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
```
```bash
# CHGRP - change group ownership
# Change the group of /u and subfiles to "admin".
$ chgrp -hR admin /u
# Change the current folder, all subfolders and files to the group "nealalan.com"
$ chgrp -hR nealalan.com .
              
```

### processes
```bash
$ systemctl start
$ systemctl stop
$ systemctl status <servicename>

# journalctl - Log file for the system to help debug when a server doesn’t start
$ journalctl -xe

# SHOW STATUS OF WHAT'S CURRENTLY RUNNING
# service <servicename> status
$ service --status-all

```

### remote connections
```bash
$ ssh -i <pem> <user>@<ip>
$ scp -i <pem> <local> <dest>
```

### users & accounts
```bash
$ adduser
$ addgroup
$ chown

# FILE ACCESS CONTROL LIST
$ getfacl <file>
$ setfacl -m u:user2:rwx example/
$ setfacl -m g:group1:rwx ./

# ADDING A NEW USER
$ sudo adduser neal
$ sudo su neal (either way)
$ cd /home/neal
$ sudo mkdir .ssh
$ sudo ssh-keygen
$ sudo usermod -aG sudo neal   // add to group sudo
$ sudo cat nealkey.pub > authorized_keys
$ sudo nano /etc/ssh/sshd_config
#     UsePAM yes
#     allowAllowUsers neal

```

## wordpress
- wordpress-online-vulnerabilitty-scanners
<br><br>

## COMMANDS 101 
Basic commands to navigate use the command line
```bash
# ECHO - write arguments to the standard output
$ echo "cat" > cat.txt
$ echo $PATH
# CAT - concatenate and print files
#  -n number the output lines starting at 1
#  -s squeeze out blank lines
#  -t -v display non-printable characters
$ cat cat.txt
$ cat cat.txt cat.txt > 2cats.txt
# HEAD
# TAIL - continue to print out an open file such as a log
$ tail -f /var/log/wifi.log
# AWK [ -F fs ] [ -v var=value ] [ 'prog' | -f progfile ] [ file ...  ]
# PS - process status
$ ps aux
$ ps -u root
# DISK USAGE
$ df -ah
# DISK USAGE by folder
$ du -sh


# LOCATE

EXPORT
$ export PATH=$PATH:$HOME/.local/bin
```
Directory linking using link / ln See also: [ln command](https://www.computerhope.com/unix/uln.htm)
```bash
# LN - link
#  -s is a symbolic link
$ sudo ln -s /home/ubuntu/sites-available sites-available
$ sudo ln -s /var/www/nealalan.com/html/ nealalan.com
```

Stream editing of data, useful with Regex to change contents of a file from the command line
```bash
# STREAM EDITOR
$ sed -f <text-commands>
# deleted 1 and 3
$ seq 10 | sed -e 1d -e 3d
$ seq 10 | sed -e '1d;3d'
# replace sour char with dest char in order
$ sed y/source-chars/dest-chars/
# replaces all numbers in format of 999-99-9999 or 9 numbers in a row
$ sed "y/123/abc/"
$ sed -ri ':1
         s/(^|[^-0-9])[0-9]{3}-[0-9]{2}-[0-9]{4}([^-0-9]|$)/\1XXX-XX-XXXX\2/g
         s/(^|[^-0-9])[0-9]{9}([^-0-9]|$)/\1XXXXXXXXX\2/g
         t1' <ssn.txt>

```

## More Useful CLI tools
- xmodulo.com/useful-cli-tools-linux-system-admins.html
```bash
# DARWIN / MAC -- DISPLAY INSTALLABLE TOOLS USING BREW
$ brew search
```

[[edit](https://github.com/nealalan/command/edit/master/README.md)]
