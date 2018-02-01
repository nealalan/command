## Commands


```bash
# DIRECTORY/FILE COLLAPSE
# find all files in this directory and its sub-directories 
# and execute mv with target directory . for each file found 
# to move them to current directory.
$ find . -mindepth 2 -type f -print -exec mv --backup=numbered {} . \;
```
```bash
# SYSTEM IO MONITORING LOOP
# writes out the activity  on the system every 3 seconts
$ white true ; do iostat -w 3 ; done
````

[View Jekyll Hacker Theme Page](https://pages-themes.github.io/hacker/)

[View Jekyll Hacker Theme Src](https://github.com/pages-themes/hacker/edit/master/index.md) 

## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/nealalan/command/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/nealalan/command/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
