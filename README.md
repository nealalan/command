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
````
## searching
``bash
# SEARCH A FILE FOR SPECIFIC CONTENT
# -H : print the filename of each match
# --max-count=#
# -c : suppress output and count matching lines
# -v : inverse matching
# -E : regex pattern search (or text search)
$ cat access.log | grep -E 'php|POST|HEAD|DNS'
```
(https://raw.githubusercontent.com/nealalan/command/master/grep-E.png)

[View Jekyll Hacker Theme Page](https://pages-themes.github.io/hacker/)

[View Jekyll Hacker Theme Src](https://github.com/pages-themes/hacker/edit/master/index.md) 

<br><br>
[edit](https://github.com/nealalan/command/edit/master/README.md)
