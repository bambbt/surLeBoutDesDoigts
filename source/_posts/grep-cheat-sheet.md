---
title: Grep cheat sheet
date: 2019-09-20 19:50:20
tags: [Terminal,Shell,Cheat sheets]
categories:
 - [Unix, Command]
---

**grep** searches the input files for lines containing a match to a given pattern list. When it finds a match in a line, it copies the lines to standard output.

# How to grep sur le bout des doigts !

## Search for a string in a file 
This is a basic usage of grep command. 
``` bash
grep Lorem index.html
```
Here, we are looking for the word "Lorem" in index.html file.

## Insensitive case search 
Searching for a word with insensitive case.
``` bash
grep -i "Lorem" index.html
```
Here, we are looking for the word Lorem written with or without upper case.

## Searching for a string in multiple files.
This command will search for "Lorem" in different files.
``` bash
grep Lorem index*.*
```
Here, we are looking for Lorem in all the files that have a name starting with "index" with all the extension available in the directory where the file is. 

##  Searching for a string using a regular expresion pattern
This one is a very powerful feature, if you use it wisely.
``` bash
grep "Lorem.*amet" index.html
```
Here, we are looking for every line that contain the pattern that starts with "Lorem" and ends with "dance", whatever is in between.

## Display line numbers.
Using the **-n** option, enable to display the line number which contains the matched pattern.
``` bash
grep -n Lorem index.html 
```

## Highlighting the result 
Using the **--color** option, enable to highlight the sucessful matches.
``` bash
grep --color Lorem index.html
```

## Search for the lines excluding a specific pattern
Using the **-v** option, enable to list all the lines that do not contain the pattern.
``` bash
grep -v Lorem index.html
```

## Search the pattern recursively 
Using the **-r** option, enable to search in all the files of a directory recursively.
``` bash
grep -r Lorem var/www/
```

## Number of times a pattern matches in a file
Using the **-c** option, enable to count the number of times a pattern matches in a file
``` bash
grep -c "Lorem ipsum" index.html
```

Here it is ! Now, you have everything on sur le bout des doigts (on the thumbs).