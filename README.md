## [nealalan.github.io](https://nealalan.github.io)/[command](https://nealalan.github.io/command)

- [iptables essentials](https://nocsma.wordpress.com/2016/10/21/iptables-essentials-common-firewall-rules-and-commands/)

## files
```bash
# DIRECTORY/FILE COLLAPSE
# find all files in this directory and its sub-directories 
# and execute mv with target directory . for each file found 
# to move them to current directory.
$ find . -mindepth 2 -type f -print -exec mv --backup=numbered {} . \;
```

## monitoring
```bash
# SYSTEM IO MONITORING LOOP
# writes out the activity  on the system every 3 seconts
$ white true ; do iostat -w 3 ; done
```
## nc / netcat / TCP & UDP connections and listener
There's a lot of stuff on search engines... i found it's useless to spend a lot of time on this command. But understand what it does.
```bash
# LISTEN FOR A CONNECTION ON PORT 42
$ nc -l 42
# CONNECT TO PORT 42 VIA THE LOOPBACK IP FROM ANOTHER TERM
$ nc 127.0.0.1 42
# either side can type and it will echo back
# terminate the connection with ^D (EOF)
```
```bash
# LISTEN INTO A FILE
$ nc -l 43 > filename.receive
# SEND A FILE TO PORT 43 VIA THE LOOPBACK IP FROM ANOTHER TERM
$ nc 127.0.0.1 43 < filename.send
```

## searching
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

[View Jekyll Hacker Theme Page](https://pages-themes.github.io/hacker/)

[View Jekyll Hacker Theme Src](https://github.com/pages-themes/hacker/edit/master/index.md) 

<br><br>
[edit](https://github.com/nealalan/command/edit/master/README.md)
