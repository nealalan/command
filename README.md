## [nealalan.github.io](https://nealalan.github.io)/[command](https://nealalan.github.io/command)

- [iptables essentials](https://nocsma.wordpress.com/2016/10/21/iptables-essentials-common-firewall-rules-and-commands/)

## Useful CLI tools
- xmodulo.com/useful-cli-tools-linux-system-admins.html


## files
```bash
# DIRECTORY/FILE COLLAPSE
# find all files in this directory and its sub-directories 
# and execute mv with target directory . for each file found 
# to move them to current directory.
$ find . -mindepth 2 -type f -print -exec mv --backup=numbered {} . \;
```
## git / github
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

## monitoring
```bash
# SYSTEM IO MONITORING LOOP
# writes out the activity  on the system every 3 seconts
$ white true ; do iostat -w 3 ; done
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

## SQL
- sqlmap

## wordpress
- wordpress-online-vulnerabilitty-scanners

[View Jekyll Hacker Theme Page](https://pages-themes.github.io/hacker/)

[View Jekyll Hacker Theme Src](https://github.com/pages-themes/hacker/edit/master/index.md) 

<br><br>
[edit](https://github.com/nealalan/command/edit/master/README.md)
