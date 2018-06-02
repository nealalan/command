# [nealalan.github.io](https://nealalan.github.io)/[command](https://nealalan.github.io/command)

- [iptables essentials](https://nocsma.wordpress.com/2016/10/21/iptables-essentials-common-firewall-rules-and-commands/)

## Mac Package Managers
```bash
# INSTALL APPLE XCODE COMMAND LINE DEV TOOLS
$ xcode-select --install
# INSTALL HOMEBREW / BREW
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# CHECK STATUS OF BREW
$ brew doctor
# INSTALL IFTOP
$ brew install iftop
```
```bash
# SEE WHAT'S INSTALLED
$ brew list && brew cask list
$ system_profiler -detailLevel full SPApplicationsDataType >> installed_software_$(date "+%Y%m%d_%H%M%S").txt
$ brew ls --full-name --versions >>  installed_software_$(date +"%Y%m%d_%H%M%S").txt
# CREATE 'Brewfile' LIST OF INSTALLS & INSTALL LIST IN 'Brewfile'
$ brew bundle dump
$ brew Brewfile
# ... IN UBUNTU
$ sudo apt list --installed >> installed_software_$(date +"%Y%m%d_%H%M%S").txt
```

## Useful CLI tools
- xmodulo.com/useful-cli-tools-linux-system-admins.html
```bash
# DARWIN / MAC -- DISPLAY INSTALLABLE TOOLS USING BREW
$ brew search
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
```bash
# SYNC FILES ACROSS COMPUTERS
$ rsync --dry-run --recursive --compress --progress --delete --itemize-changes |
~/Pictures/ Neal@192.168.0.103:/Users/neal/Pictures/All_Photos > |
~/Desktop/pic_bkp_$(date +"%Y%m%d_%H%M%S").txt
```

## git / github / hub

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

## curl 
```bash
# Find system settings from the command line
$ curl http://169.254.169.254/
```

## monitoring
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

## networking 

### nc / netcat / TCP & UDP connections and listener
There's a lot of stuff on search engines... i found it's useless to spend a lot of time on this command. But understand what it does.

```bash
# LISTEN FOR A CONNECTION ON PORT 42
# i add -v to everything because I like verbosity
$ nc -v -l 42
# CONNECT TO PORT 42 VIA THE LOOPBACK IP FROM ANOTHER TERM
$ nc -v 127.0.0.1 42
# either side can type and it will echo back
# terminate the connection with ^D (EOF)
```
```bash
# LISTEN INTO A FILE
$ nc -v -l 43 > filename.receive
# SEND A FILE TO PORT 43 VIA THE LOOPBACK IP FROM ANOTHER TERM
$ nc -v 127.0.0.1 43 < filename.send
```
```bash
### netstat -- show active connections (port) and sockets
$ netstat -a | more
```

### nethogs
```bash
# NETHOGS -- monitor process socket connections 
```

### nslookup - useless?
```bash
# QUERY INTERNET NAME SERVERS
# returns the domain name server the IP to domain resolution came from
# -type=SOA : find out the server of authority = might not work
$ nslookup neonaluminum.com
```

### whois - use this versus nslookup
```bash
# QUERY IANA.ORG FOR DOMAIN INFO
$ whois neonaluminum.com
```

### dig
```bash
# DOMAIN INFORMATION GATHERING
# primarily used for DNS queries of A, TXT, MX, SOA, NS record sets
$ dig neonaluminum.com
# trace trace the domain server of authority (SOA)
$ dig +trace neonaluminum.com
# pull the DNS records (use A, TXT, MX, SOA, NS, ANY)
$ dig neonaluminum.com ANY +noall +answer
```

### local info
```bash
$ nmap localhost
$ scutil --proxy
$ scutil --dns
$ scutil --get ComputerName
```

### maven
apache maven will build your jar files from java source packages. 
```bach
# from your project-dir/pom.xml folder
$ mvn package
# you should end up with BUILD SUCCESSFUL and a folder project-dir/target/
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
``` 

## searching
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

## SQL
- sqlmap

## Upgrading
```bash
# Mac
$ brew upgrade
# Ubuntu
$ apt update
$ apt upgrade
```

## images
```bash
# ExifTool - Read, Write and Edit Meta Info 
# Info: https://www.sno.phy.queensu.ca/~phil/exiftool/
# Install:
$ brew install exiftool

# Use:

```

## wordpress
- wordpress-online-vulnerabilitty-scanners
<br><br>



[[edit](https://github.com/nealalan/command/edit/master/README.md)]
